---
created: 2023-11-07 16:38
modified: Tuesday 7th November 2023 16:39:04
alias:
---
up::
tags:: #class-validator #validation #api

## class-validator.ValidateNested

```ts
import { Field, InputType } from '@nestjs/graphql';
import * as Validator from 'class-validator';
import { BookCreateInput } from '../../generated-db-types';
import { Type } from 'class-transformer';

@InputType()
export class UserBookCountResoinse {
  @Validator.ValidateNested()
  @Field(() => BookCreateInput, { nullable: true })
  @Type(() => BookCreateInput)
  book: BookCreateInput;

  @Field(() => String, { nullable: true })
  @Validator.IsString()
  count: string;
}
```


### Resources
[GitHub - typestack/class-validator: Decorator-based property validation for classes.](https://github.com/typestack/class-validator)
