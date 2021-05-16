---
title: "Rust"
date: "2021-02-11T18:19:55"
description: "Anki deck for Rust cards."
draft: true
# image: /path/to/image
css: custom-styles.css
---

# Rust

## Why do we use `mut` in rust?

Because all variables are immutable by default.

## What does `::` mean in a function call like String::new()?

That we are calling an associated function (read static function from other languages), which is defined on the type not on the instance.

`new()` is a common function used to create a new object of a certain type.rust

## How do you import a library in rust?

You add the library using `use libraryName` for example `use std::io`

## How do you run a rust program while developing it?

You use `cargo run`

## How do you build a rust program for release?

You use `cargo build --release`

## How do you check that a rust program compiles without creating an executable?

You use `cargo check`.
Useful because it's faster than building an executable.

## How do you generate documentation for crates used in your project?

You use `cargo doc --open`

## How do you print values using println?

You can pass any number of values to `println` and they will fill in empty brackets `{}`.

```rust
println!("The number is: {}", number);
```

## What does an exclamation mark mean in rust before parentheses?

An exclamation mark is used to indicate that a function call is actually a macro.

## What is `cmp` in rust?

Compare is a method that can be called on anything that can be compared. It returns one of `std::cmp::Ordering`.

## What are the `std::cmp::Ordering` enums in rust?

`Less`, `Greater`, and `Equal`.


## What is a match expression in rust?

A match expression contains *arms*.
Each *arm* contains a *pattern* and code which will run if the value at the beginning of the match expression fits that arm's pattern.

## How do you convert a string to a number in rust?

Using `parse` method on the string.
You need to specify the type of number.
`let number: u32 = string.parse().expect("failed to parse")` would parse the string in the variable string into an unsigned 32bit integer called number.

## What are the two values on the Result enum in rust?

`Ok` which contains the value and `Err` which contains the error.