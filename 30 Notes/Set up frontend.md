---
created: 2024-05-19 19:23
modified: 2025-06-15T21:10:08-04:00
alias: 
---
up::  [[How to start a programming project]]
tags:: [[frontend development]]
source::
## Set up frontend


**Set up frontend** ([Next.js Typescript Starter](https://github.com/jpedroschmitz/typescript-nextjs-starter?tab=readme-ov-file))
```
cd apps
pnpm create next-app -e https://github.com/jpedroschmitz/typescript-nextjs-starter
```

**Set up linting** **husky**
[Get started | Husky](https://typicode.github.io/husky/get-started.html)
[ESLint, Prettier, husky and lint-staged - DEV Community](https://dev.to/shashwatnautiyal/complete-guide-to-eslint-prettier-husky-and-lint-staged-fh9#:~:text=Husky%20is%20a%20pre%2Dcommit,of%20the%20file%20before%20committing.)

**Add scripts to package.json**
```
    "scripts": {
        "start:web": "pnpm exec nx dev web",
        "lint:web": "pnpm exec nx lint web",
        "lint:fix:web": "pnpm exec nx lint:fix web",
        "test": "echo \"Error: no test specified\" && exit 1",
        "prepare": "husky install"
    },
```
**Set up github**
```
git init
# add husky to monorepo root
# create repo push to repo
```



**How to set up next.js with apollo client**
[https://medium.com/@sehrawy/how-to-set-up-nextjs-14-with-apollo-client-754a177e0a00](https://medium.com/@sehrawy/how-to-set-up-nextjs-14-with-apollo-client-754a177e0a00)

[https://github.com/apollographql/next-apollo-example](https://github.com/apollographql/next-apollo-example)

[https://stackoverflow.com/questions/78141234/unable-to-setup-next-js-14-with-apollo-client-graphql](https://stackoverflow.com/questions/78141234/unable-to-setup-next-js-14-with-apollo-client-graphql)

[https://egghead.io/lessons/next-js-connect-a-frontend-next-js-application-to-a-serverless-fauna-database-with-apollo-client](https://egghead.io/lessons/next-js-connect-a-frontend-next-js-application-to-a-serverless-fauna-database-with-apollo-client)

**Sources**
