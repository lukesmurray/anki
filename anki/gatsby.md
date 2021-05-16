---
title: "Gatsby"
date: "2020-12-30T08:21:31"
description: "Anki deck for Gatsby cards."
draft: true
# image: /path/to/image
css: custom-styles.css
---

# Gatsby

## In Gatsby what parameters are passed to a page object in the create page API?

- path - the path to the page, starts with a forward slash
- matchPath - an alternative path to the page (optional)
- component - the component used to render the page
- context - data passed to the component in `props.pageContext`

## When you create pages in Gatsby what data do you want to pass in the page context?

You want to pass the minimal amount of data necessary to determine what to query within the context of the page.

It is much better to collocate queries for data within the component than to structure your data in the `createPage` API.

## In Gatsby how do you limit the data returned from an `allNodes` query?

You can limit the number of nodes returned from an `allNodes` query using the `limit` argument.

```graphql
allMarkdownRemark(limit: 3) {
  ...
}
```

## In Gatsby how do you skip the data returned from an `allNodes` query?

You can skip over a number of results from an `allNodes` query by using the `skip` argument.

```graphql
allMarkdownRemark(skip: 3) {
  ...
}
```

## In Gatbsy how do you filter data returned from an `allNodes` query?

Using `filter` syntax.

```graphql
allMarkdownRemark(filter: { field1: { eq: "foo" }, field2: { eq: "bar" } }) {
  ...
}
```

<!-- ## In Gatsby what operators are supported by filter?

-   `eq`: short for **equal**, must match the given data exactly
-   `ne`: short for **not equal**, must be different from the given data
-   `regex`: short for **regular expression**, must match the given pattern. Note that backslashes need to be escaped *twice*, so `/\w+/` needs to be written as `"/\\\\w+/"`.
-   `glob`: short for **global**, allows to use wildcard `*` which acts as a placeholder for any non-empty string
-   `in`: short for **in array**, must be an element of the array
-   `nin`: short for **not in array**, must NOT be an element of the array
-   `gt`: short for **greater than**, must be greater than given value
-   `gte`: short for **greater than or equal**, must be greater than or equal to given value
-   `lt`: short for **less than**, must be less than given value
-   `lte`: short for **less than or equal**, must be less than or equal to given value
-   `elemMatch`: short for **element match**, this indicates that the field you are filtering will return an array of elements, on which you can apply a filter using the previous operators -->

## In Gatsby how do you pass variables to a page component query?

By setting the variables in the page context.

## What is a Node in Gatsby?

<!-- TODO(lukemurray): see https://www.gatsbyjs.com/docs/reference/config-files/actions/#createNode for better documentation -->

A node is a data structure used to model all data in Gatsby.

A node has the following special fields.

- `id` - a globally unique id for the node
- `parent` - key used to point to the source for this node, null if this is a source node
- `children` - key used to point to an array of nodes which are sourced from this node
- `internal`
  - `contentDigest` - a hash of the content used for caching
  - `mediaType` - optional media type used to indicate to transformer plugins whether or not this node has content they can process
  - `type` - a globally unique node type used for schema generation. i.e. `type` and `allType`
  - `content` - the content of the node
  - `description` - a description of the node used for diagnostic error messages
- `[key: string]` - any fields specific to the node

## What are parent child relationships in gatsby?

Parent child relationships are used to record where data is sourced from in Gatsby.

The parent is the source for any child nodes.

An example is a parent node may be a `File` and the child node may be a `MarkdownRemark` node created by the `gatsby-transformer-remark` plugin.

## How are foreign keys specified in Gatsby?

Foreign keys are any field on a node which contain a `___NODE` suffix.

These fields are expected to contain an `id` of a node.

At query time the `id` is resolved to the `Node`.

## How are schema root fields generated in Gatsby?

Gatsby generates two root fields for every Node type.

For example given a node type `User` Gatsby will create two root fields `user` and `allUser`.

## What arguments do plural root fields accept in gatsby?

`filter`, `sort`, `skip`, and `limit`

## What arguments do singular root fields accept in gatsby?

Singular root fields accept the same arguments as `filter`.

```graphql
file(path: {ne: "/"})
```

If multiple nodes pass the filter one is selected at random.

## How do you pass filters in Gatsby using arguments?

Filters are created using `TypeQueryOperatorInput` for example `StringQueryOperatorInput`


## How do you pass sorts in Gatsby using arguments?

Sorts are created using `TypeSortInput` for example `MdxSortInput`


## How do you create custom types in Gatsby?

Using the `createTypes` action in the `createSchemaCustomization` export in `gatsby-node.js`.

`createTypes` accepts type definitions.

<!-- TODO(lukemurray): continue from https://www.gatsbyjs.com/docs/reference/graphql-data-layer/schema-customization/ -->