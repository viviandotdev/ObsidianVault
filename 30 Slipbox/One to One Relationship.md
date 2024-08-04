---
created: 2023-09-27 19:44
modified: Wednesday 27th September 2023 19:44:00
alias:
---
up::
tags:: #database #prisma
Related: [[Database Relationships]]

## One to One Relationship

### Example
The `bookIsbn` relation scalar is a direct representation of the foreign key in the underlying database. This one-to-one relation expresses the following:

- "a book can have zero userBook or one userBook" (because the `userBook` field is [optional](https://www.prisma.io/docs/concepts/components/prisma-schema/data-model#type-modifiers) on `Book`)
- "a userBook must always be connected to one book"

```
model Book {
    id          String    @id @default(uuid())
    /// @Validator.IsString()
    title       String
    /// @Validator.IsString()
    author      String?
    /// @Validator.IsString()
    pubDate     String?
    /// @Validator.IsString()
    publisher   String?
    /// @Validator.IsString()
    coverImage  String?
    /// @Validator.IsString()
    description String?
    /// @Validator.IsInt()
    pageNum     Int?
    /// @Validator.IsString()
    isbn        String    @unique
    /// @Validator.IsString()
    categories  String?
    // One to One
    userBook    UserBook?
}

model UserBook {
    id           String       @id @default(uuid())
    userId       String
    bookIsbn     String       @unique
    status       String
    rating       Int?
    dateStarted  String?
    dateFinished String?
    // One to One
    book         Book         @relation(fields: [bookIsbn], references: [isbn])
    // Many to One
    user         User?        @relation(fields: [userId], references: [id], onDelete: Cascade)
    // Optional back reference that will not be used
    ShelfEntry   ShelfEntry[]
}

```

### Resources
[One-to-one relations](https://www.prisma.io/docs/concepts/components/prisma-schema/relations/one-to-one-relations)
