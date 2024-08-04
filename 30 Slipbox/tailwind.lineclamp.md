---
created: 2024-03-15 12:16
modified: Friday 15th March 2024 12:16:26
alias:
---
up::
tags:: #tailwind
links::
## tailwind.lineclamp

[Line Clamp - Tailwind CSS](https://tailwindcss.com/docs/line-clamp)

Truncating multi-line text
Can also truncate single line
Use line clamp instead of truncate it is easier to use

```jsx
  <div className='flex flex-col justify-between'>
                            <div className='flex flex-col gap-0.5'>
                                <div className='line-clamp-2 text-base font-medium text-beige-700'>
                                    {book?.title}
                                </div>
                                <div className='text-gray-400'> {formatAuthors(book!)}</div>
                            </div>
                            <div className='text-xs text-gray-400'>
                                Completed On Jul 23, 2022
                            </div>
                        </div>
```
