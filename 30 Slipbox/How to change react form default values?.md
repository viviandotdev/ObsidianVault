---
created: 2023-10-13 17:39
modified: Friday 13th October 2023 17:39:58
alias:
---
up::
tags::  #useform #react #react-hook-form

## How to change react form default values?

**In a nutshell:** You need to define your defaultValues in the `userForm`.
```javascript

  const displayFormSchema = z.object({
    shelves: z.array(z.string()).refine((value) => value.some((item) => item), {
      message: "You have to select at least one item.",
    }),
  });

  type DisplayFormValues = z.infer<typeof displayFormSchema>;

  const form = useForm<DisplayFormValues>({
    resolver: zodResolver(displayFormSchema),
    defaultValues: useMemo(() => {
      return {
        shelves: userBook.shelves.map((item) => item.shelf.name),
      };
    }, [userBook.shelves]),
  });
```
- `useMemo` recalculates the default values whenever `userBook.shelves` changes, ensuring the form displays the correct initial values.
**Change Affecting `useMemo`:**
- **Use Case:** The user navigates to a different page and then comes back to the bookshelf page, triggering a refetch of bookshelf data.
- **Impact on `useMemo`:** When the user navigates back to the bookshelf page, the `useMemo` hook will recalculate the default values based on the new bookshelf data fetched from the server. This ensures that the form displays the correct default values for the user's shelves.
Then you need to listen to potential change.
```javascript
  useEffect(() => {
    form.reset({ shelves: userBook.shelves.map((item) => item.shelf.name) });
  }, [userBook.shelves])
```
- `useEffect` resets the form with the updated `userBook.shelves` data, ensuring the form stays in sync with the latest user bookshelf data.
- In this case, the effect is resetting the form values using the `form.reset` method provided by `react-hook-form`.
- The `useEffect` has a dependency array `[userBook.shelves]`, meaning it will trigger the effect only when `userBook.shelves` changes.
**Change Affecting `useEffect`:**
- **Use Case:** The user adds a new shelf from another part of the application, triggering an update to the `userBook.shelves` data.
- **Impact on `useEffect`:** When the user adds a new shelf, the `useEffect` hook will reset the form with the updated `userBook.shelves` data. This ensures that the form is reset with the latest shelves whenever a new shelf is added, providing an up-to-date user experience.

[javascript - How to change React-Hook-Form defaultValue with useEffect()? - Stack Overflow](https://stackoverflow.com/questions/62242657/how-to-change-react-hook-form-defaultvalue-with-useeffect)

[useForm](https://react-hook-form.com/docs/useform#defaultValues)
