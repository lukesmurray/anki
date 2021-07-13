---
title: "Declarative Interaction"
date: "2021-07-08T09:02:22"
description: "Anki deck for Declarative Interaction cards."
draft: true
# image: /path/to/image
css: custom-styles.css
---

# Declarative Interaction

## What are the top level keys of a concepts file in declarative interaction?

"concepts", "actions", "triggers", "behaviors", and "extensions"

```json
{
    "concepts": {},
    "actions": {},
    "triggers": {},
    "behaviors": {},
    "extensions": []
}
```

## What are the top level keys of a concept in declarative interaction?

"schema", "actions", "triggers", and "behaviors"

```json
{
    "concepts": {
        "schema": {},
        "actions": {},
        "triggers": {},
        "behaviors": {},
    }
}
```

## How do you pass arguments to an action in declarative interaction?

You call the action with `"actionName": {"argumentName": "argumentValue"}`

Example in a behavior clause

```json
{
    "behaviors": {
        "behaviorName": {
            "when": [],
            "then": [
                { "actionName": {"argumentName": "argumentValue"} }
            ]
        }
    }
}
```

## What are the top level keys of a behavior in declarative interaction?

"when" and "then"

```json
{
    "behaviors": {
        "when": [],
        "then": []
    },
}

```

## What is the difference between a mapping file and a concept file in declarative interaction?

The mapping file can contain "views"

## How do you access the return value of an action in a variable in declarative interaction?

1. Use the syntax `"as": "variableName"` and then access the variable with `$variableName`
2. Omit the `"as"` key and access the variable using `$actionName`. This is the value from the most recent call to the action `actionName`

## How do you access a variable in declarative interaction?

Use the syntax `$variableName`

## What is the scope of variables in declarative interaction?

The variable exists for the duration of an event.



