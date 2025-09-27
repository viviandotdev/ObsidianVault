---
created: 2024-05-19 19:24
modified: 2025-07-02T07:44:08-04:00
---
up::  [[How to start a programming project]]
tags::  [[backend development]]
source::

**Set up the backend**
```
//Clone the nestjs typescript starter git clone
https://github.com/nestjs/typescript-starter
//install dependencies
pnpm install

# For Express and Apollo (default) $ npm i @nestjs/graphql @nestjs/apollo @apollo/server graphql
```
[GraphQL + TypeScript | NestJS - A progressive Node.js framework](https://docs.nestjs.com/graphql/quick-start)

how to set up graphql + apollo backend in nestjs


**Set up the prisma database**
install and init
```
npm install prisma --save-dev
npx prisma init
```


[[How to set up prisma with local docker container]]


**Create database tables**
add model to `schema.prisma` file
```groovy
model User {
  id    Int     @default(autoincrement()) @id
  email String  @unique
  name  String?
}
```

generate SQL migration files and run again the database, this create the model User and its properties in your database. **you should run this command when there is change to the prisma models to update your database.**

```
pnpm --filter api exec prisma migrate dev
```
check the database to see the user model is added
```
pnpm --filter api exec prisma studio
```

**Install and generate prisma client**
Prisma client is a database client that is generated from the prisma model definition, **you will need to run this command after every change to your prisma models to update the client**
```
npm install @prisma/client
```
Reads your Prisma schema and updates the generated Prisma Client library
```
pnpm --filter api exec prisma generate
```


**Updating the `prisma.schema`**

- add new models or properties `add validators` for all inputs (without adding validators the input won’t be detected when passed through graphQL)
    - `prisma generate` updates your Prisma Client to match your latest Prisma schema. This ensures your Client is in sync before running migrations.
    - run `prisma migrate` to keep the database schema in sync with the prisma schema, also updates the `generate-db-types`
    - If you don't run `prisma generate` after changing your schema, `prisma migrate` may not work as expected, since it will be using an outdated Client that doesn't match the schema.

**How to add a new resource**

- `nest g resources` {resource name}
    - select graphql (code first)
- update the ``

`autoSchemaFile` out o. 80000f sync (`api/src/schema.gql`)

1. **end the server**
2. remove dist folder
3. re run the build
4. **start the server agin**

ending and starting the server is what generate the schema file

9bfd9fec-bf64-4ec0-9d0e-688591b7513b

### Resource

[Nestjs and Prisma](https://docs.nestjs.com/recipes/prisma)

[Prisma Client](https://www.prisma.io/docs/concepts/components/prisma-client/working-with-prismaclient/generating-prisma-client)
