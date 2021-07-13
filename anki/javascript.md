---
title: "javascript"
date: "2021-05-17T13:00:56"
description: "Anki deck for javascript cards."
draft: true
# image: /path/to/image
css: custom-styles.css
---

# javascript

<div markdown="block" data-question>

## Identify the missing javascript built in type

- {{c1::null}}
- {{c2::undefined}}
- {{c3::boolean}}
- {{c4::number}}
- {{c5::string}}
- {{c6::object}}
- {{c7::symbol}}

</div>

## Which javascript built in type is not a primitive?

Object

## What does typeof operator do in javascript?

The typeof operator inspects the type of the given value, and returns a string.

<div markdown="block" data-question>

## What does the following code evaluate to in javascript?

```js
typeof null
```
</div>

The string `"object"`

## How do you test for null using typeof

Check that the value is false and that `typeof` the value is "object"

`(!a && typeof a === "object")`

<div markdown="block" data-question>

## What does the following code evaluate to in javascript?

```js
typeof function a() {}
```
</div>

The string `"function"`

## What does the `length` property evaluate to on a function in javascript?


The number of parameters it is declared with

<div markdown="block" data-question>

## What does the following code evaluate to in javascript?

```js
typeof [1,2,3]
```
</div>

The string `"object"`

## What is the difference between an undefined and undeclared variable in javascript?

An undefined variable has been declared in the accessible scope but has no value in it.

An undeclared variable has not been declared in scope.


```js
var a;
a; // undefined
b; // undeclared
```

## What does the following code evaluate to in javascript?

```js
var a;
typeof a;
typeof b;
```
</div>

```js
var a;
typeof a; // "undefined"
typeof b; // "undefined"
```

## Why is `typeof` an undeclared variable useful in javascript?

You can test to see if a variable is declared by checking if it `typeof` that variable is undefined.

```js
if (typeof DEBUG !== "undefined") {
  console.log("Debug Mode")
}
```

