---
title: "Shell"
date: "2020-12-25T08:45:35"
description: "Anki deck for Shell cards."
draft: true
# image: /path/to/image
---

# Shell

## How do you create a symbolic link to a file in unix?

```sh
ln -s source_file link_file
```

## How do you create a symbolic link to a directory in unix?

```sh
ln -s source_directory link_directory
```

## What is the difference between single quotes and double quotes in bash?

Single quotes do not interpolate anything but double quotes do.

```bash
WORD="Hello World"
echo "${WORD}"
> Hello World
echo '${WORD}'
> ${WORD}
```

## What does the `$` do for variables in bash?

When you want to use a variable in bash, such as assign it or export it you write the variable name without a `$`

When you want to use the value in a variable you write the variable name with a `$` prefix.

## What is parameter expansion in bash?

Parameter expansion occurs when a variable is surrounded by `${  }`.
Parameter expansion occurs before the command entered into bash is called and before word splitting occurs.

Because parameter expansion occurs before word splitting if a parameter would expand to contain white space you need to surround it with quotes in order for it to remain a single argument.

## What is command substitution in bash?

Command substitution occurs when a command is surrounded by `$( )`

The command is run in a sub shell and the `$( )` is replaced with the output of the command.


## How do you declare an array in bash?

An array is a space separated list of strings nested in parentheses.

```bash
array=(one two three four five)
```

## What is brace expansion in bash?

Brace expansion is used to generate ranges of strings or all possible combinations of a set of strings.

**Ranges**

```bash
echo {1..10}
> 1 2 3 4 5 6 7 8 9 10
echo {a..z}
> a b c d e f g h i j k l m n o p q r s t u v w x y z
```

Note that brace expansion has two dots between `<START>` and `<STOP>` and that brace expansion is inclusive.

**Combinations**

```bash
echo {a,b}.js
> a.js
> b.js
```

## What is word splitting in bash?

Word splitting refers to the process of splitting a string entered into a bash shell into multiple separate strings.

The splitting occurs on white space.