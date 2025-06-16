---
created: 2023-10-30 19:26
modified: 2025-06-13T08:38:40-04:00

Category: react
status: idea
---
up::  [[frontend development]]
tags:: [[react]]
## How to structure react applications

### Project Structure
Well structured applications are more productive to work on because they are easy to navigate, modify and scale.
Place most of the application code under`src` directory. This separates the application code from the project configuration files such as `package.json`, `next.config.js` and `tsconfig.js` which should remain the root of the project.
```shell
|-- src                   # most of the application code
	|-- components        # shared components used across the entire application
	|-- config            # all the global configuration, env variables etc. get exported from here and used in the app
	|-- modules           # feature based modules
	|-- hooks             # shared hooks used across the entire application
	|-- lib               # re-exporting different libraries preconfigured for the application
	|-- providers         # all of the application providers
	|-- app               # app router
	|-- stores            # global state stores
	|-- test              # test utilities and mock server
	|-- types             # base types used across the application
	|-- utils             # shared small reusable, generic functions
# project configuration files
|-- package.json
|-- next.config.js
|-- tsconfig.js
|-- tailwind.config.ts
```
### Module Structure
In order to scale the application easily, modularize it by splitting the application into self-contained modules that represent major features or top level routes. This improves navigation and keeps related functionalities together.
This modular organization streamlines development by allowing you to quickly locate files relevant to the current task. For example, all dashboard-related files can be found in the dashboard module, allowing for quick access when working on that feature.
```shell
src/modules/dashboard
|-- api         # exported API request declarations and api hooks related to a specific feature
|-- components
|-- templates
|-- hooks
|-- types
|-- index.ts    # main entry point of the module.
```
**templates**
	templates files are compositions of components and provide a structured layout for the feature.
**components**
	reusable react components specific to this module
**hooks**
	hosts the custom hooks specific to this module
**api**
	API logic specific to this feature such as calculations or data manipulation logic
**templates**
	hosts templates
**types**
	TypeScript type declarations that are specific to the dashboard module. It can include interfaces, types, or enums.


### Resources

[React Architecture: How to Structure and Organize a React Application | Tania Rascia](https://www.taniarascia.com/react-architecture-directory-structure/)

[Notion Link](https://www.notion.so/architecture-create-application-modules-60dfdd9315b9431abceb05b028182099?pvs=4)
[https://github1s.com/xXValhallaCoderXx/tao-react-app-structure/blob/HEAD/src/pages/products/list/slice/dux.js](https://github1s.com/xXValhallaCoderXx/tao-react-app-structure/blob/HEAD/src/pages/products/list/slice/dux.js)

[https://github.com/ericdiviney/react-handbook](https://github.com/ericdiviney/react-handbook)
[https://github.com/alan2207/bulletproof-react](https://github.com/alan2207/bulletproof-react)

[https://github1s.com/AllStackDev1/github-user-search/blob/HEAD/src/components/ErrorButton.tsx](https://github1s.com/AllStackDev1/github-user-search/blob/HEAD/src/components/ErrorButton.tsx)

[bulletproof-react](https://github.com/alan2207/bulletproof-react)

nextjs medusa[https://github1s.com/medusajs/nextjs-starter-medusa/blob/HEAD/src/modules/checkout/components/shipping/index.tsx#L28](https://github1s.com/medusajs/nextjs-starter-medusa/blob/HEAD/src/modules/checkout/components/shipping/index.tsx#L28)
