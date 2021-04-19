---
title: "Javascript"
date: "2020-12-30T10:58:41"
description: "Anki deck for Javascript cards."
draft: true
# image: /path/to/image
---

# Javascript

## How do you create a symbol in javascript?

You create a symbol using either `Symbol(<key>)` or `Symbol.for(<key>)` where `<key>` is a unique string identifying the symbol.

`Symbol(<key>)` creates a symbol unique to the current realm and will not collide with a Symbol created for the same key in another realm.

`Symbol.for(<key>)` creates a cross-realm symbol in the symbol registry which can be used in any realm.


## How does the replacer parameter work in the `JSON.stringify` method in javascript?

The `replacer` parameter takes two parameters the key and the value being stringified.

If you return a `Number`, `String`, `Boolean` or `null` the stringified version of that value is used as the property value.

If you return `Function`, `Symbol` or `undefined` the property is not included in the output.

If you return an `Object` the replacer is called recursively on the object.

## How does the reviver parameter work in the `JSON.parse` method in javascript?

The reviver is called recursively from the most nested properties to the least nested properties.

The input to the reviver is the property name and the property value.

If the reviver returns undefined the property is deleted from the object.

The `this` keyword can be used in the reviver to refer to the object containing the property.

## What is the difference between `instanceOf` and `typeof` in javascript?

`instanceOf` is a binary operator which takes an object and a *constructor*.
`instanceOf` return a boolean determining if the object has the constructor in it's prototype chain.

`typeof` is a unary operator which takes a single argument and returns a string representing the type of that argument.

## How could you JSON serialize symbols in javascript?

If the symbols are used as property names you need to create a `toJSON` method on the object you are serializing and convert the symbol values into something serializable such as a string.

If the symbols are property values you need to override the replacer parameter in `JSON.stringify` to replace the symbols with something serializable such as a string.

In either case when you revive the object you need to convert the replaced strings back into symbols. You can perform the revival in the reviver parameter of the `JSON.parse` method.

The best way to encode the symbols is by retaining the symbol key in the serialized representation of the symbol.

```ts
function serializeSymbol(s: Symbol) {
  return `@@${Symbol.keyFor(s)}@@`
}

const REGEX_SYMOBL_STRING = /^@@(.*)@@$/;
function deserializeSymbol(s: String) {
  let match = REGEX_SYMOBL_STRING.test(value);
  if (match) {
      return Symbol.for(match[1])
  }
}
```

*Note: In this example the symbols must be created in the global registry because Symbol.keyFor returns the symbol key from the global registry.*

## Is null json serializable?

Yes when you call `JSON.stringify(null)` it outputs `null`. If you call `JSON.parse("null")` you get `null`.

## How do you round a number to a certain number of decimal places in javascript?

call `toFixed()` on the number.

```js
var num = 5.678
console.log(num.toFixed(2))
// logs 5.68
```
