---
modified: 2025-06-06T10:34:27-04:00
---

### Getting Started

**Install the dependencies**
```
pnpm install
```

**Initialize the databasee**
```
cd server
```

```
pnpm drizzle:generate
```

```
pnpm drizzle:migrate
```

```
pnpm drizzle:seed
```

**Errors**
[Error: Could not locate the bindings file. · Issue #146 · WiseLibs/better-sqlite3](https://github.com/WiseLibs/better-sqlite3/issues/146)

```
cd server
pnpm run dev
```

```
cd client
pnpm run dev
```