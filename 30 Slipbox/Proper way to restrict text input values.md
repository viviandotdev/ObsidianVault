---
created: 2023-08-10 17:27
modified: Thursday 10th August 2023 17:29:32
alias:
---
up::
tags:: #angular #html
related:
## Proper way to restrict text input values

This function restricts all special characters and only allows alphabets and numbers

```javascript
 public inputValidator(event: any) {
    //console.log(event.target.value);
    const pattern = /^[a-zA-Z0-9]*$/;
    //check if the input matches the mattern
    if (!pattern.test(event.target.value)) {
      event.target.value = event.target.value.replace(/[^a-zA-Z0-9]/g, "");
      // if input does not match make the input match
    }
  }

<input type="text" [(ngModel)]="abc.abc (input)="inputValidator($event)" />
```


### Resources
[angular - Proper way to restrict text input values (e.g. only numbers) - Stack Overflow](https://stackoverflow.com/questions/37435529/proper-way-to-restrict-text-input-values-e-g-only-numbers)
