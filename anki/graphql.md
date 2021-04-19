---
title: "Graphql"
date: "2020-12-25T08:45:46"
description: "Anki deck for Graphql cards."
draft: true
# image: /path/to/image
---

# Graphql

## What is the syntax for passing arguments to fields in Graphql?

Use parentheses after the field name with a comma separated list of names followed by a colon and a value.
These arguments are unordered.

```graphql
{
  user(id: 4) {
    id
    name
    profilePic(width: 100, height: 50)
  }
}
```

## What are the three types of operations allowed in Graphql?

- *query* – a read‐only fetch.
- *mutation* – a write followed by a fetch.
- *subscription* – a long‐lived request that fetches data in response to source events.

## Describe the building blocks of a basic graphql query operation

```graphql
# the query operation with variables
query queryName(variable: VariableType) {
  # the selection set

  # a field in the selection set with an argument
  field(argument: ArgumentValue) {

    # a field alias and a nested field in the selection set
    fieldAlias: NestedField

  }
}
```

## What is the purpose of a fragment in graphql?

A fragment allows for reuse of common selections of fields.

For example this fragment selects the id, name, and profile picture on the user field.

```graphql
query withFragments {
  user(id: 4) {
    friends(first: 10) {
      ...friendFields
    }
    mutualFriends(first: 10) {
      ...friendFields
    }
  }
}

fragment friendFields on User {
  id
  name
  profilePic(size: 50)
}
```

## What is a type condition of a fragment in graphql?

When you define a fragment you specify the name and the type the fragment is defined for.

```graphql
# name pageFragment
# defined on type Page
fragment pageFragment on Page {

}
```

The selection defined by a fragment will only return values when the object the fragment is operating on matches the type the fragment applies to.

## What is the syntax used to define inline fragments in graphql?

Use `...` followed by `on Type` and then the selection in brackets.

```graphql
user {
  follows {
    ... on User {
      name
    }
    ... on Page {
      title
    }
  }
}
```

## Why would you use inline fragments in graphql?

In order to conditionally select fields based on the object the fragment is operating on.

Fragment selections are only defined when the object the fragment is operating on matches the type the fragment applies to.

Consider the following query.

```graphql
user {
  follows {
    ... on User {
      name
    }
    ... on Page {
      title
    }
  }
}
```

The user may follow other users and pages.
When the user follows a page the inline fragment for Page is defined and we get the title of the page.
When the user follows another User the user fragment is applied and we get the name of the followed user.

## How are variables passed to a graphql query?

Variables are provided at the top of an operation and are in scope throughout the operation.

```graphql
query getUser($name: String) {
  user(name: $name) {
    id
  }
}
```
## What is the scope of variables in a graphql operation?

Variables have a global scope within a graphql operation.
Variables can be accessed within fragments as long as the variable is defined in the top level the operation the fragment is operating on and the variable has the same name.

## How are default values given to variables in graphql queries?

Using the syntax `Variable: Type = DefaultValue`

Here is an example of giving the variable `$id` a default value of `0`.

```graphql
query getUser($id: Int = 0) {
  user(id: $id) {
    name
  }
}
```

## What are the two directives supported by any spec compliant graphql server?

- `@include(if: Boolean)` Only include this field in the result if the argument is `true`.
- `@skip(if: Boolean)` Skip this field if the argument is `true`.

## Give an example of using the @include directive in graphql

The directive comes after arguments.

```graphql
query profile($id: ID, $withMyInfo: Boolean!) {
  me: user(id: $id) @include(if: $withMyInfo) {
    id
    name
    email
  }
  picture
}
```

The directive is often used with variables to the query.

```graphql
query UserInfo($id: Int, $withFriends: Boolean!) {
  user(id: $id) {
    name
    friends @include(if: $withFriends) {
      name
    }
  }
}
```


## What are the built in Scalar types in graphql?

- *Int* - represents a 32 bit signed integer
- *Float* - represents a signed double
- *String* - represents utf-8 text data
- *Boolean* - represents true or false. Uses booleans if supported else integers 1 and 0.
- *ID* - represents a unique identifier. Used as keys, must be serializable to a string but can be a numeric value.

## How are non-null and nullable fields specified in graphql?

Non null fields are specified by adding a trailing exclamation mark after the type.

```graphql
name: String!
```

All other fields are nullable and null is a valid response type.

## What is the difference between how query fields are executed and mutation fields are executed?

While query fields are executed in parallel, mutation fields run in series, one after the other.

This means that if we send two `incrementCredits` mutations in one request, the first is guaranteed to finish before the second begins, ensuring that we don't end up with a race condition with ourselves.

## What is the special `__typename` field in graphql?

The `__typename` field is used to determine the type of object returned by a query.
This can be helpful for narrowing union types.

## How do you define a custom type in a graphql schema?

Using the syntax `type TYPENAME`

```graphql
type User {
  name: String!
  id: Int
}
```

## How do you define an array type in a graphql schema?

Using the type modifier `[]` around the type. For example `[Type]`.


```graphql
type User {
  name: String!
  id: Int
  friends: [Int]! # array of user ids
}
```

An exclamation mark on the outside of the Array indicates that the field will never return null, it will always at least return an empty array.

An exclamation mark in the array will mean that the entries in the array are always non null.

## Does graphql use semicolons at the end of lines?

No!

```graphql
type User {
  name: String!
  id: Int
}
```

## How do you define arguments on graphql fields?

Using the syntax `(argumentName: ArgumentType)` or  `(argumentName: ArgumentType = DefaultValue)`

```graphql
type User {
  name: String!
  id: Int
  friends(close: Boolean = false): [Int]!
}
```

## What is the query type in a graphql schema?

The query type defines the set of allowable Queries.
The query type essentially defines the root fields which can be used in queries.

A service which has the following schema supports querying for heros and droids, and passing arguments to those objects.

```graphql
type Query {
  hero(episode: Episode): Character
  droid(id: ID!): Droid
}
```

## How do you define the root type in a graphql schema?

In a schema the  query type is defined as

```graphql
schema {
  query: Query
}
```

## How do you define a custom scalar type in graphql schema?

Using the syntax `scalar SCALAR_TYPE`

You must then define how that type is serialized, deserialized, and validated.

## How do you define an enum type in a graphql schema?

```graphql
enum Episode {
  NEWHOPE
  EMPIRE
  JEDI
}
```

## What is an interface in a GraphQL schema?

An interface is an abstract object type which can be implemented by concrete object types.

The interface defines a set of fields that a concrete type must include to implement the interface.

## How do you define and use an interface in a graphql schema?

You define the interface with `interface INTERFACE_NAME` and you implement the interface using `type TYPE_NAME implements INTERFACE_NAME`.

```graphql
interface Identifiable {
  id: ID!
}

type User implements Identifiable {
  id: ID!
  name: string!
}
```

## In graphql when querying a field defined as an interface how do you access fields unique to the concrete types which implement that interface?

You must use an inline fragment applied to the concrete type to access the concrete type's fields.

```graphql
# field which is defined as an interface type
interfaceField {
  # field defined on the interface type
  FieldOnInterface
  ...on ConcreteClass {
  # field defined only on a concrete type
    FieldOnConcreteClass
  }
}
```

## How do you define a Union type in a graphql schema?

You use the syntax `union UNION_NAME = CLASS_1 | CLASS_2 | CLASS_3`

## What are the limitations of the union type in a graphql schema?

You can only use Concrete Types in a union.
You cannot use interfaces or other unions in the union.

## How do you query fields of a union type in a graphql schema?

You use inline fragments for the fields specific to  each of the union types.
For common fields you can make the Types inherit from a common interface and use an inline fragment on that interface.

```graphql
{
  search(text: "an") {
    __typename
    ... on Character {
      name
    }
    ... on Human {
      height
    }
    ... on Droid {
      primaryFunction
    }
    ... on Starship {
      name
      length
    }
  }
}
```

## How do you define input types in a graphql schema?

You define an input type using the syntax `input INPUT_TYPE {...}`

```graphql
input ReviewInput {
  stars: Int!
  commentary: String
}
```

## In a graphql schema can you use object types as fields in input types?

No! Why? Because Object types have tons of rich features such as unions, interfaces, and arguments none of which are appropriate as inputs.
The input Objects have a separate type from Object types.

Input Objects can never be used as Output objects and Output Objects can never be used as Input Objects.


## Does graphql support recursive queries or definitions?

No! Why? Because GraphQL cannot check for cycles and if recursive queries or definitions were allowed then cyclical queries could be used to attack graphql servers.

## How do you define a nested array in a graphql schema?

Using nested array syntax.


`[[Int]]` would be a valid type for an array such as `[[1,2], [3,4]]`

## What are schema root fields in graphql?

The root fields are the entry point of any graphql query.

The root fields define the set of possible queries that can be issued to a graphql server.

<!-- TODO(lukemurray): add docs for connections https://relay.dev/graphql/connections.htm -->