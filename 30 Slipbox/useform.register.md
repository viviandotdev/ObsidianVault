---
created: 2023-09-22 19:32
modified: Friday 22nd September 2023 19:33:10
alias:
---
up::
tags:: #useform #react

## useform.register

This method allows you to register an input or select element and apply validation rules to React Hook Form.

``` typescript
const { onChange, onBlur, name, ref } = register('firstName');
// include type check against field path with the name you have supplied.

<input
  onChange={onChange} // assign onChange event
  onBlur={onBlur} // assign onBlur event
  name={name} // assign name prop
  ref={ref} // assign ref prop
/>

// same as above but much simplier
<input {...register('firstName')} />
```

```tsx
import * as React from "react";
import { useForm } from "react-hook-form";


export default function App() {
  const { register, handleSubmit, formState: { errors }, } = useForm({
    defaultValues: {
      firstName: '',
      lastName: '',
    }
  });


  return (
    <form onSubmit={handleSubmit(console.log)}>
      <input
		{...register("firstName", { required: true })}
		placeholder="First name"
		className={`${errors[id] ? "border-rose-500" : "border-neutral-300"}`}
         />

      <input
	    {...register("lastName", { minLength: 2 })}
	    placeholder="Last name"
	    className={`${errors[id] ? "border-rose-500" : "border-neutral-300"}`}
	  />

      <input type="submit" />
    </form>
  );
}
```

[useForm - register](https://react-hook-form.com/docs/useform/register)
