---
modified: 2025-06-13T08:39:27-04:00
---

tags:: [[react]]
# React Application Structure & Best Practices

## 1. Folder Structure Overview

### Modules
- Represent main application features or domains.
- Contain containers and feature-specific components.
- Example: `src/modules/checkout`, `src/modules/userProfile`

### Components
- **Layout-specific components:**  
  Used strictly for page layout, placed under route-specific folders.  
  Example:  
  ```
  src/app/_route_/(components)/_component_
  ```
- **Shared components:**  
  Used across multiple features or modules.  
  Example:  
  ```
  src/components/_component_
  ```

### Hooks
- Store custom React hooks that encapsulate business logic or reusable behaviors.
- Extract as much logic as possible into hooks to keep components clean.
- Examples of use cases:
  - API calls
  - IntersectionObserver for element visibility
  - Wrapping external API responses for a cleaner component API

```js
function useSalesAnalytics(date) {
  const { loading, data, refetch } = useQuery(GET_SALES, {
    variables: { date },
  });

  if (!data) {
    return { loading, sales: { total: 0 }, refetch };
  }

  return {
    loading,
    refetch,
    sales: aggregate(data),
  };
}
```

### API
- Contains business/domain-specific API functions.
- These functions wrap generic API calls and add domain logic like calculations or data manipulation.
- Keeps API logic decoupled from UI and generic utilities.

### Utils
- Contains small, reusable, generic utility functions.
- Should be decoupled from business logic and React.
- Examples:
  - `validateEmail(email)`
  - `sortCollectionByAttribute(collection, attribute)`

### Store (State Management)
- State stores should be decoupled from features.
- Multiple features can consume the same store.
- Example:  
  - `userStore` is shared by `userProfile`, `userEditForm`, `userPreferences` features.
- Avoid grouping stores inside feature folders to keep them reusable and modular.

### Templates
- Store page templates that compose components into page layouts.



## 2. Data Fetching Code

- Prefer placing data fetching logic inside **custom hooks** (in the `hooks` folder).
- This abstracts API calls and business logic away from components.
- Example: `useSalesAnalytics` hook shown above.
- API calls themselves should be in the `api` folder, with business-specific logic applied there.

---

## 3. State Management

- Use stores (e.g., Zustand, Redux) to manage global or shared state.
- Keep stores separate from feature folders.
- Features consume stores but do not own them.
- This promotes reusability and separation of concerns.

---

## 4. Restructuring Recommendations

- Create a `modules` folder for main features.
- Keep routes inside `src/app` or `src/pages` depending on your framework.
- Place layout components inside route-specific `(components)` folders.
- Shared components go into `src/components`.
- Extract business logic into hooks and API folders.
- Keep generic utilities in `src/utils`.
- Keep state stores in a dedicated `src/stores` folder.

---

## 5. Example Folder Structure

```
src/
  app/
    (main)/
      order/
        confirmed/
          [id]/
            loading.tsx
          (components)/
            OrderSummary.tsx
  components/
    Button.tsx
    Modal.tsx
  modules/
    checkout/
      components/
      hooks/
      api/
      store/
    userProfile/
      components/
      hooks/
      api/
      store/
  hooks/
    useSalesAnalytics.ts
    useIntersectionObserver.ts
  api/
    salesApi.ts
    userApi.ts
  stores/
    userStore.ts
    cartStore.ts
  utils/
    validateEmail.ts
    sortCollectionByAttribute.ts
  templates/
    MainPageTemplate.tsx
```

---

## 6. Additional Resources

- [Bulletproof React](https://github.com/alan2207/bulletproof-react)
- [React Handbook](https://github.com/ericdiviney/react-handbook)
- [Zustand Store Best Practices](https://www.reddit.com/r/reactjs/comments/15agnsv/zustand_where_to_place_files_selectors_stores_how/)
- [Next.js Medusa Starter Example](https://github1s.com/medusajs/nextjs-starter-medusa/blob/HEAD/src/app/(main)/order/confirmed/[id]/loading.tsx)
