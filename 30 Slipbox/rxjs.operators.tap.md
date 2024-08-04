---
created: <% tp.file.creation_date() %>
modified: <% tp.file.last_modified_date("dddd Do MMMM YYYY HH:mm:ss") %>
alias:
---
up::
tags:: #rxjs
related:

# Tap

*Tap is most commonly used for console logging. *You can place a tap(console.log) anywhere in your observable pipe, log out the notifications as they are emitted by the source returned by the previous operation.

**Example**
Check a random number before it is handled. Below is an observable that will use a random number between 0 and 1, and emit 'big' or 'small' depending on the size of that number. But we wanted to log what the original number was, so we have added a tap(console.log).

```
  import { of, tap, map } from 'rxjs';

  of(Math.random()).pipe(
    tap(console.log),
    map(n => n > 0.5 ? 'big' : 'small')
  ).subscribe(console.log);
```

```
 selectedPlan$: Observable<PlanSelection> = this._store$.pipe(
    select(getSelectedPlan),
    tap((selectedPlan: PlanSelection) => (console.log(selectedPlan))),
    filter<PlanSelection>((v) => !!v),
  )
```

### Resources
https://rxjs.dev/api/index/function/tap
