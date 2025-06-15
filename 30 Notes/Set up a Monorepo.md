up::[[How to build and deploy a sass]]
**Set up a Monorepo**

Initialize new pnpm workspace
```
mkdir <project-name> 
cd <project-name> 
pnpm init
```

create a `pnpm-workspace.yaml` file at the root of the project that defines the monorepo structure
```
packages: 
	- 'apps/*' 
```

Install **nx** at the root level `package.json` to run operations across the entire monorepo
```
pnpm add nx -D -w

```

**Running tasks with nx**
```
pnpm exec nx <target-command> <project-name> 
pnpm exec nx start api

//Across all porjects 
pnpm exec nx run-many --target=build --all 
//Across selected projects 
pnpm exec nx run-many --target=build --projects=api,web
```

**Additional Resources**
[https://dev.to/nx/setup-a-monorepo-with-pnpm-workspaces-and-speed-it-up-with-nx-1eem#initialize-a-new-pnpm-workspace](https://dev.to/nx/setup-a-monorepo-with-pnpm-workspaces-and-speed-it-up-with-nx-1eem#initialize-a-new-pnpm-workspace)
[https://pnpm.io/installation](https://pnpm.io/installation)
[https://levelup.video/tutorials/monorepos-with-pnpm/versioning-and-workspace-pinning](https://levelup.video/tutorials/monorepos-with-pnpm/versioning-and-workspace-pinning)