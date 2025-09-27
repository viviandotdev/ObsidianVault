---
created: 2023-10-13 11:20
modified: 2025-06-15T18:51:35-04:00

---
tags:: [[prisma]] [[database]]

Create and connect
### Schema
```ts
model UserBook {
    /// @Validator.IsString()
    id           String            @id @default(uuid())
    /// @Validator.IsString()
    userId       String
    /// @Validator.IsString()
    bookId       String
    /// @Validator.IsString()
    status       String //WANT TO READ, READ, READING, DID NOT FINISH, UP NEXT
    /// @Validator.Min(1)
    /// @Validator.Max(5)
    /// @Validator.IsInt()
    rating       Int?
    // Many to One: many user books belong to one book when book
    book         Book?             @relation(fields: [bookId], references: [id], onDelete: Cascade)
    shelves      UserBookShelves[]

    /// @Validator.IsString()
    /// @Validator.ValidateNested()
    @@unique(fields: [userId, bookId], name: "identifier")
}

model UserBookShelves {
    userBook   UserBook @relation(fields: [userBookId], references: [id])
    userBookId String
    shelf      Shelf    @relation(fields: [shelfId], references: [id])
    shelfId    String

    @@id([userBookId, shelfId])
}

model Shelf {
    /// @Validator.IsString()
    id        String            @id @default(uuid())
    /// @Validator.IsString()
    name      String
    // Many to One: many shelves belong to one user when user is deleted all shelves are deleted as well
    user      User?             @relation(fields: [userId], references: [id], onDelete: Cascade)
    // Many to Many: a single shelf can be associated with multiple userBooks,
    userBooks UserBookShelves[]

    /// @Validator.IsString()
    /// @Validator.ValidateNested()
    @@unique(fields: [userId, name], name: "identifier")
}

```

### Update many to many
- Updates `UserBook`
- **`deleteMany`**: It deletes all existing `UserBookShelves` records related to the original `UserBook` (identified by `origin.id`).
- **`create`**: Creates new `UserBookShelves` records based on the `shelfList`.
	- Each shelf name is mapped to an object with `connectOrCreate` logic, ensuring that the shelf is either connected to the user or created if it doesn't exist.
```ts
  async update(args: {
    data: UserBookUpdateInput;
    where: UserBookIdentifierCompoundUniqueInput;
  }) {
    const { userId, bookId } = args.where;

    const origin = await this.findUnique(args.where);
    const shelfList = args.data.shelves;
    const updateUserBook = await this.repository.update({
      where: {
        identifier: {
          userId,
          bookId,
        },
      },
      data: {
        status: args.data.status,
        rating: args.data.rating,
        shelves: {
          deleteMany: { userBookId: origin.id },
          create: shelfList?.map((name: string) => {
            return {
              shelf: {
                connectOrCreate: {
                  where: { identifier: { userId, name } },
                  create: { name },
                },
              },
            };
          }),
        },
      },
      include: {
        book: true,
        shelves: {
          include: {
            shelf: true,
          },
        },
      },
    });
    return updateUserBook;
  }

```



### Resources
[[Database Relationships]]
[Many-to-many relations | Prisma Docs](https://www.prisma.io/docs/concepts/components/prisma-schema/relations/many-to-many-relations)
[GitHub1s](https://github1s.com/jimleestone/next-real-world/blob/HEAD/lib/api/mutation/article.mutation.ts)
	article.mutations.ts
		updateArticle
[typescript - Prisma many-to-many relations: create and connect - Stack Overflow](https://stackoverflow.com/questions/65950407/prisma-many-to-many-relations-create-and-connect)
