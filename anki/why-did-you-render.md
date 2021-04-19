---
title: "Why Did You Render"
date: "2021-01-04T11:47:36"
description: "Anki deck for Why Did You Render cards."
draft: true
# image: /path/to/image
---

# Why Did You Render

## How do you add why did you render logging to a component?

```tsx
const Component = props => <div>{props.children}</div>

Component.whyDidYouRender = true; // use default options

// OR

Component.whyDidYouRender = { // use custom options
  logOnDifferentValues: true,
  customName: 'ComponentName'
}
```


