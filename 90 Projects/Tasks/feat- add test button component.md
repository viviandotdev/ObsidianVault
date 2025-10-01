how to add test-button component to the registry

### Component Library

**Step 1**
`packages/example-library/src/components/ui/*` **to create your components**
	- add a new component here
**Step 2**
`packages/example-library/src/examples/*` to update the example components
	- then add the example component here
**Export the example component **
`packages/example-library/src/examples/index.ts`
```
export * from './red-button/red-button-primary';
export * from './red-button/red-button-secondary';
export * from './test-button';
```
This is where the docs can access this component

**Step 1.5**
- `packages/example-library/src/blocks/*` to update the examples blocks


**Step 3**
- `apps/docs/registry.json` to update the registry with the new component

**Step 4 build the registry**
```
pnpm run registry
```
**this creates the component.json file here**
apps/docs/public/r

**Step 5- create the test-button.mdx file**

### Part 2: Add Component to showcase
**Step 1** update the apps/showcase/registry.json to match the docs
**Step 2** build the registry
```
pnpm run registry
```
**this creates the component.json file here**
apps/showcase/public/r
**Step 3:** Create file in apps/showcase/app/components
**example-test.tsx**
**Step 4:** update 
