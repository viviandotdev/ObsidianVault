---
modified: 2025-07-20T21:08:45-04:00
---

## Overview

[tRPC](https://trpc.io/) enables end-to-end typesafe APIs, allowing you to build and consume APIs without schemas, code generation, or runtime errors. These rules will help you follow best practices for tRPC v11.

## Project Structure

For a clean tRPC setup, follow this recommended structure:
```
.
├── src
│   ├── pages
│   │   ├── _app.tsx  # add `createTRPCNext` setup here
│   │   ├── api
│   │   │   └── trpc
│   │   │       └── [trpc].ts  # tRPC HTTP handler
│   │   ├── server
│   │   │   ├── routers
│   │   │   │   ├── _app.ts  # main app router
│   │   │   │   ├── [feature].ts  # feature-specific routers
│   │   │   │   └── [...]
│   │   │   ├── context.ts   # create app context
│   │   │   └── trpc.ts      # procedure helpers
│   │   └── utils
│   │       └── trpc.ts  # typesafe tRPC hooks
```

## Server-Side Setup

### Initialize tRPC Backend

```typescript
// server/trpc.ts
import { initTRPC } from '@trpc/server';

// Initialize tRPC backend (should be done once per backend)
const t = initTRPC.create();

// Export reusable router and procedure helpers
export const router = t.router;
export const publicProcedure = t.procedure;
```

### Create Router

```typescript
// server/routers/_app.ts
import { z } from 'zod';
import { router, publicProcedure } from '../trpc';

export const appRouter = router({
  // Your procedures here
  greeting: publicProcedure
    .input(z.object({ name: z.string() }))
    .query(({ input }) => {
      return `Hello ${input.name}`;
    }),
});

// Export type definition of API (not the router itself!)
export type AppRouter = typeof appRouter;
```

## Client-Side Setup

### Next.js Integration

```typescript
// utils/trpc.ts
import { httpBatchLink } from '@trpc/client';
import { createTRPCNext } from '@trpc/next';
import type { AppRouter } from '../server/routers/_app';

function getBaseUrl() {
  if (typeof window !== 'undefined') return ''; // browser should use relative path
  if (process.env.VERCEL_URL) return `https://${process.env.VERCEL_URL}`; // SSR should use vercel url
  return `http://localhost:${process.env.PORT ?? 3000}`; // dev SSR should use localhost
}

export const trpc = createTRPCNext<AppRouter>({
  config() {
    return {
      links: [
        httpBatchLink({
          url: `${getBaseUrl()}/api/trpc`,
          // Include auth headers when needed
          async headers() {
            return {
              // authorization: getAuthCookie(),
            };
          },
        }),
      ],
    };
  },
  ssr: false, // Set to true if you want to use server-side rendering
});
```

## Best Practices

1. **Use Zod for Input Validation**: Always validate procedure inputs with Zod for better type safety and runtime validation.

    ```typescript
    import { z } from 'zod';

    procedure
      .input(z.object({
        id: z.string().uuid(),
        email: z.string().email(),
        age: z.number().min(18)
      }))
      .mutation(({ input }) => { /* your code */ })
    ```

2. **Organize Routers by Feature**: Split your routers into logical domains/features rather than having one large router.

    ```typescript
    // server/routers/user.ts
    export const userRouter = router({
      list: publicProcedure.query(() => { /* ... */ }),
      byId: publicProcedure.input(z.string()).query(({ input }) => { /* ... */ }),
      create: publicProcedure.input(/* ... */).mutation(({ input }) => { /* ... */ }),
    });

    // server/routers/_app.ts
    import { userRouter } from './user';
    import { postRouter } from './post';

    export const appRouter = router({
      user: userRouter,
      post: postRouter,
    });
    ```

3. **Use Middleware for Common Logic**: Apply middleware for authentication, logging, or other cross-cutting concerns.

    ```typescript
    const isAuthed = t.middleware(({ next, ctx }) => {
      if (!ctx.user) {
        throw new TRPCError({ code: 'UNAUTHORIZED' });
      }
      return next({
        ctx: {
          // Add user information to context
          user: ctx.user,
        },
      });
    });

    const protectedProcedure = t.procedure.use(isAuthed);
    ```

4. **Use Proper Error Handling**: Utilize tRPC's error handling for consistent error responses.

    ```typescript
    import { TRPCError } from '@trpc/server';

    publicProcedure
      .input(z.string())
      .query(({ input }) => {
        const user = getUserById(input);
        if (!user) {
          throw new TRPCError({
            code: 'NOT_FOUND',
            message: `User with id ${input} not found`,
          });
        }
        return user;
      });
    ```

5. **Use Data Transformers**: Use SuperJSON for automatic handling of dates, Maps, Sets, etc.

    ```typescript
    import { initTRPC } from '@trpc/server';
    import superjson from 'superjson';

    const t = initTRPC.create({
      transformer: superjson,
    });
    ```

6. **Leverage React Query Integration**: For React projects, use tRPC's React Query utilities for data fetching, mutations, and caching.

    ```tsx
    function UserProfile({ userId }: { userId: string }) {
      const { data, isLoading, error } = trpc.user.byId.useQuery(userId);

      if (isLoading) return <div>Loading...</div>;
      if (error) return <div>Error: {error.message}</div>;

      return <div>{data.name}</div>;
    }
    ```

7. **Context Creation**: Create a proper context object to share resources across procedures.

    ```typescript
    // server/context.ts
    import { inferAsyncReturnType } from '@trpc/server';
    import * as trpcNext from '@trpc/server/adapters/next';
    import { prisma } from './prisma';

    export async function createContext({
      req,
      res,
    }: trpcNext.CreateNextContextOptions) {
      const user = await getUser(req);
      return {
        req,
        res,
        prisma,
        user,
      };
    }

    export type Context = inferAsyncReturnType<typeof createContext>;
    ```

8. **Type Exports**: Only export types, not the actual router implementations, from your server code to client code.

    ```typescript
    // Export type router type signature, NOT the router itself
    export type AppRouter = typeof appRouter;
    ```

9. **Procedure Types**: Use different procedure types for different authorization levels.

    ```typescript
    export const publicProcedure = t.procedure;
    export const protectedProcedure = t.procedure.use(isAuthed);
    export const adminProcedure = t.procedure.use(isAdmin);
    ```

10. **Performance Optimization**: Use batching and prefetching for optimized data loading.

    ```typescript
    // Client-side batching in Next.js setup
    httpBatchLink({
      url: `${getBaseUrl()}/api/trpc`,
      maxURLLength: 2083,
    })

    // Prefetching data in Next.js
    export async function getStaticProps() {
      const ssg = createServerSideHelpers({
        router: appRouter,
        ctx: {},
      });

      await ssg.post.byId.prefetch('1');

      return {
        props: {
          trpcState: ssg.dehydrate(),
        },
        revalidate: 1,
      };
    }
    ```

## Version Compatibility

This guide is for tRPC v11, which requires:
- TypeScript >= 5.7.2
- Strict TypeScript mode (`"strict": true` in tsconfig.json)

## Further Resources

- [Official Documentation](https://trpc.io/docs)
- [GitHub Repository](https://github.com/trpc/trpc)
- [Example Apps](https://trpc.io/docs/example-apps)
