`useState` is a _hook_. A hook is a special type of function that allows us to "hook into" React internals. We'll learn much more about hooks later in this course.

The `useState` hook returns an array containing two items:

1. The current value of the state variable. We've decided to call it `count`.
    
2. A function we can use to update the state variable. We named it `setCount`.

What exactly is the difference between these two forms?

```
// Form 1:

const [count, setCount] = React.useState(

window.localStorage.getItem('saved-count')

);

// Form 2:

const [count, setCount] = React.useState(() => {

return window.localStorage.getItem('saved-count');

});
```


The difference in how javascript works between these two forms.
