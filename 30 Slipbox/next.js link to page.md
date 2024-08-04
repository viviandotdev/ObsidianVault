---
created: 2024-02-15 07:48
modified: Thursday 15th February 2024 07:48:34
alias:
---
up::
tags:: #nextjs
links::
## next.js link to page


```ts
const linkRef = useRef<HTMLAnchorElement>(null);
```


```ts
<Link ref={linkRef} href={`/test1/book/${book?.id}/activity`} className="hidden"></Link>
```


```ts
onClick={(e) => {
	e.stopPropagation();
	if (linkRef.current) {
		linkRef.current.click();
	}
}}
```
