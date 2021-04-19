---
title: "jq"
date: "2021-01-05T14:31:52"
description: "Anki deck for jq cards."
draft: true
# image: /path/to/image
---

# jq

## What does the jq . filter do?

The `.` filter is the identity filter.

It takes the input and produces it unchanged as output.

## What is a jq object identifier index filter?

`.foo` or `.foo.bar`.

When given a JSON object as input it produces the value of the key foo or null if there is non present.

## What is the jq array index filter?

`.[2]`

When given a JSON array as input it produces the value of the index or null if there is non present.

`.[-1]` gets the last element, `.[-2]` the second to last, and so on.
`.[0]` gets the first element.

## What is the jq Object Value iterator?

`.[]` gets the values of an array or object one at a time.

## What does the comma do in jq?

If multiple filters are separated by a comma then the same input is fed to both and the two filters' output streams are concatenated in order. First all outputs from the left expression, then all outputs from the right expression.

## What does the pipe do in jq?

The pipe operators feeds the outputs of the left filter into the input of the right filter.

## How can you construct an array in jq?

You surround a set of elements with `[]`.
The elements can be known values `[.foo, .bar]` or results of a filter `[.items[].name]`.

## How can you construct objects in jq?

Using the syntax `{key: value}`.
The values can be expressions `{"name": .user}` and the keys can be expressions if they are surrounded with parentheses `{(.user): .titles}`

## How can you express equals or not equals in jq?

`==` is equals

`!=` is not equals


