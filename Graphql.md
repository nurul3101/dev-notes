## Graphql

- GraphQL is a query language for APIs and a runtime for fulfilling those queries with your existing data
- Graphql is an API Standard
- Enables declarative data fetching - client specifies exactly what data it wants from an API.
- Graphql server exposes single end point and responds to queries with precisely data that a client asked for

- Graphql has strong type system which give us an idea of capabilities of an API.
- Schema Definition Language(SDL) language is used to define schema of an API.
``` javascript
type Person{
  name: String!
  age: Int!
  posts: [Post!]!
}
  
type Post{
  title:String!
  author:Person!
}
     
/* Example of a query */          
{
  allPersons {
    name
  }
}
```
- Here allPersons is the root field of the query. Everything that follows the root field is the payload.
- In GraphQL, each field can have zero or more arguments if that’s specified in the schema.

## Important concepts of graphql

- Schema
- Query
- Mutation
- Subscription
- Resolver function

- Generally, a schema is simply a collection of GraphQL types. However, when writing the schema for an API, there are some special root types


```js
  /* Schema Example */
type Query {
  allPersons(last: Int): [Person!]!
}

type Mutation {
  createPerson(name: String!, age: Int!): Person!
}

type Subscription {
  newPerson: Person!
}

type Person {
  name: String!
  age: Int!
  posts: [Post!]!
}

type Post {
  title: String!
  author: Person!
}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwNjM5NDQ1NzNdfQ==
-->