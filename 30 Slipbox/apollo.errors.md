---
created: 2024-01-28 08:28
modified: Sunday 28th January 2024 08:28:50
alias:
---
up::
tags:: #apollo

## apollo.errors

[Handling operation errors - Apollo GraphQL Docs](https://www.apollographql.com/docs/react/data/error-handling/)

```ts
 const { data, errors } = await client.mutate<UpdateUserMutation>({
    mutation: UpdateUserDocument,
    variables: {
      data: {
        ...values,
      },
    },
  });

  if (errors) {
    return { error: errors?.map((e) => e.message)[0] };
  }
```


**Error Policy**
none (default) - errors is returned and `data` is set to undefined even if the server returns a partial response
ignore - errors is not populated and any returned data is cached and rendered as if no errors occurred
all - both `data` and `errors` is populated you can render fro the partial results and the error information
