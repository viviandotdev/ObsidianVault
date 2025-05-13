---
created: 2023-10-07 21:18
modified: 2025-05-13T07:59:06-04:00
alias: 
---
up::
tags:: #prisma #backend #graphql

## What does prisma include do

```ts
@Mutation(() => Article, { nullable: true }) @UseGuards(GraphqlAuthGuard, AuthorGuard) async deleteArticle( @Args('where') where: ArticleWhereUniqueInput, @GraphqlFields() fields: PlainObject, ) { const article = await this.service.findUnique({ where }); if (!article) { throw new NotFoundException( `Article ${JSON.stringify(where)} do not exists`, ); } return this.service.delete({ where, include: { author: Boolean(fields.author), tags: Boolean(fields.tags), }, }); }
```


In GraphQL, the `include` argument is commonly used to specify additional fields that should be included in the response when fetching a related object. It's a way to request nested data and retrieve information about related entities in a single GraphQL query. In the context of your `deleteArticle` mutation resolver:

typescriptCopy code

`return this.service.delete({     where,     include: {         author: Boolean(fields.author),         tags: Boolean(fields.tags),     }, });`

Here's what's happening:

1. **`include` Argument**: The `include` argument is an object that specifies which related fields should be included in the response. In this case, it includes `author` and `tags` fields.

2. **`Boolean(fields.author)` and `Boolean(fields.tags)`**: These expressions are used to dynamically determine whether the related `author` and `tags` fields should be included based on the client's request. If `fields.author` and `fields.tags` are truthy (e.g., `true`), the related fields will be included in the response. If they are falsy (e.g., `false`), the fields won't be included.

3. **Response**: The `delete` method of `this.service` is likely returning the deleted `Article` object or a status indicating the success of the deletion operation. By including the related fields (`author` and `tags`) in the response, the client can receive information about these related entities along with the deleted article.


For example, if a client requests a deletion of an article and includes the `author` and `tags` fields, the response might look like this:

jsonCopy code

`{   "id": "123",   "title": "Example Article",   "author": {     "id": "456",     "name": "John Doe"   },   "tags": [     {       "id": "789",       "name": "Technology"     },     {       "id": "101",       "name": "GraphQL"     }   ] }`

In this response, the deleted article's `author` and `tags` fields are included because the client requested them using the `include` argument. This helps clients optimize their GraphQL queries by fetching all necessary data in a single request.
