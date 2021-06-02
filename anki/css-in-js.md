---
title: "Css In JS"
date: "2021-06-02T08:27:12"
description: "Anki deck for Css In JS cards."
draft: true
# image: /path/to/image
css: custom-styles.css
---

# Css In JS

<div markdown="block" data-question>
## What does the `&` do in the following styled component example?

```jsx
const Button = styled.button`
  display: flex;
  &:hover {
    color: red;
  }
`;
```
</div>

The ampersand is replaced with the class name which is generated for the button.

```css
.abc123 {
  display: flex;
}

/* replaced with the class */
.abc123:hover {
  color: red;
}
```

## What is an interpolation function in styled-components?

A function in a tagged template literal which takes `props` and returns a value for a css property.

```tsx
const Wrapper = styled.button`
  color: ${props => props.color};
  padding: 16px 24px;
`;
```

## How can you use CSS Variables to pass inline styles to styled components?

Pass the css variable in the `style` prop and use the css variable in the styled component template literal.

```tsx
const Button = ({ color, onClick, children }) => {
  return (
    <Wrapper onClick={onClick} style={{ '--color': color }}>
      {children}
    </Wrapper>
  );
}
const Wrapper = styled.button`
  color: var(--color);
  padding: 16px 24px;
`;
```

<div markdown="block" data-question>
## How would you apply custom styles to the following `TextLink` components when it is inside the `Quote` component.


```tsx
const Quote = styled.blockquote`
/* ... */
`

const TextLink = styled.a`
/* ... */
`
```
</div>

Reference the quote component in the `TextLink` styles.

This maintains the encapsulation of TextLink styles.


```tsx
const Quote = styled.blockquote`
/* ... */
`

const TextLink = styled.a`
${Quote} & {

}
`
```

<div markdown="block" data-question>
## What does the `${Quote} &` do in the following styled component example?

```tsx
const Quote = styled.blockquote`
/* ... */
`

const TextLink = styled.a`
${Quote} & {

}
`
```
</div>

The ampersand is replaced with the class name which is generated for the `TextLink` and the `${Quote}` is replaced with the class name generated for the quote.

```css

.quote123 {

}

.textLink123 {
}

.quote123 .textLink123 {
  /* rules here target text links inside quotes! */
}
```