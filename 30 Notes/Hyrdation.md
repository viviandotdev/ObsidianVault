---
created: 2023-09-23 09:57
modified: Saturday 23rd September 2023 09:57:55
alias:
---
up::
tags:: #nextjs #frontend #web-dev

## Hydration

Hydration is a technique that converts static HTML to a fully interactive React page by attaching event listeners.

During this step, Next.js **matches** the rendered HTML on the server with the corresponding React components on the client

Hydration errors occur when there is an i**nconsistency between what is being rendered on the server and on the client**. The most common reason for this is when client side constructs like use State, use Effect hooks are using in server rendered code.
