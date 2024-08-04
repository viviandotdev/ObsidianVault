---
created: 2024-06-08 18:16 
modified: Saturday 8th June 2024 18:16:00
alias: 
---
up::  
type:: #note/atomic🌳 
links::
## React.createElement
```js
const element = React.createElement(
  'p',
  { id: 'hello' },
  'Hello World!'
);
```

`React.createElement` is a function that accepts 3 or more arguments:

1. The type of the element to create.
2. The properties we want this element to have
3. The element's contents, what the element should have as children.
    

This function returns a “React element”. React elements are plain old JavaScript objects. If we inspect it with `console.log(element)`, we'll see something like this:

```ts
{

  type: "p",

  key: null,

  ref: null,

  props: {

    id: 'hello',

    children: 'Hello World!',

  },

  _owner: null,

  _store: { validated: false }

}
```


### Links to this page
These notes point directly to this note. But this note doesn't point back.
```dataview
LIST
FROM [[#]]
and !outgoing([[#]])
and -#map

SORT file.link asc
```



