---
title: "Typescript"
date: "2021-01-07T09:29:04"
description: "Anki deck for Typescript cards."
draft: true
# image: /path/to/image
---

# Typescript

## How does the Extract utility type work in typescript?

`Extract<Type, Union>` constructs a type by extracting from `Type` all union members that are assignable to `Union`.

`Type` is usually a union, and `Union` is the members of the union that you want in your final type.

```ts
type T0 = Extract<"a" | "b" | "c", "a" | "f">;
//    ^ = type T0 = "a"
type T1 = Extract<string | number | (() => void), Function>;
//    ^ = type T1 = () => void
```