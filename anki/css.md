---
title: "css"
date: "2021-05-17T13:01:22"
description: "Anki deck for css cards."
draft: true
# image: /path/to/image
css: custom-styles.css
---

# css

<div markdown="block" data-question>
What is the property in the following css rule?

```css
p {
  margin: 32px;
}
```
</div>

`margin`

<div markdown="block" data-question>
What is the selector in the following css rule?

```css
p {
  margin: 32px;
}
```
</div>

`p`

## What is a css selector?

It is the part of a css rule that describes elements the rule will match.

<div markdown="block" data-question>
What is the first declaration in the following css rule?

```css
.code-snippet {
  padding: 32px;
  white-space: pre-wrap;
}
```
</div>

`padding: 32px;`


## What is a css declaration?

A css declaration is a property value pairing.

### Example

`padding: 32px;`

## What is a css rule?

A css selector and set of css declaration.

### Example

```css
div {
    border    : 1px solid black;
    font-size : 18px;
}
```

## How would you express a css media query to apply css rules when the window has a width between 0px and 300px?

Use `max-width: 300px`

```css
@media (max-width: 300px) {
  /* your rule */
}
```

## How would you express a css media query to apply css rules when the window has a width greater than 450px?

Use `min-width: 450px`

```css
@media (min-width: 450px) {
  /* your rule */
}
```

<div markdown="block" data-question>
What does the selector `div span` select in css?
</div>

All spans which have a div as an ancestor.


<div markdown="block" data-question>
Would the selector `div span` select the span in the following html?

```html
<div>
  <section>
    <span></span>
  </section>
</div>
```
</div>


Yes.

The selector selects all spans which have any ancestor (parent, parents parent, etc...) which is a div.

<div markdown="block" data-question>
How would you write a css selector to select the direct children `li` elements of a `ul` element?
</div>

`ul > li`

<div markdown="block" data-question>
Does the selection `ul > li` select the `li` in the following html?

```html
<ul>
  <div>
    <li></li>
  </div>
</ul>
```
</div>

No.

`li > ul` only selects `ul` elements which are a direct child of a `li` element.

## What is the difference between a css property that inherits and a css property that does not inherit?

A css property that inherits is applied to an element and the element's children.

A css property that does not inherit is not passed down to the element's children.

<div markdown="block" data-question>
What color will the paragraph text be given the following css stylesheet?

```css
p {
  color: black;
}

p {
  color: red;
}
```
</div>

red

## What is the clock trick for css short hands?

Many css short hands are specified in clockwise order `Top`, `Right`, `Bottom`, `Left`. You can picture these values being assigned in order around a clock.

## How does the css clock trick for css short hands deal with missing values?

Missing values are mirrored. If you specify `top` and `right` the `top` is mirrored to the bottom and the `right` is mirrored to the `left`. If you specify `top right bottom` only the `right` is mirrored to the left.

<div markdown="block" data-question>
## Which part of the box model is blank in the following image (1)?

![](box-model-missing-1.png)
</div>




Margin

<div markdown="block" data-question>
## Which part of the box model is blank in the following image (2)?

![](box-model-missing-2.png)
</div>

Border

<div markdown="block" data-question>
## Which part of the box model is blank in the following image (3)?

![](box-model-missing-3.png)
</div>

Padding

<div markdown="block" data-question>
## Which part of the box model is blank in the following image (4)?

![](box-model-missing-4.png)
</div>

Content

<div markdown="block" data-question>

## What are the dimensions of the box in the following example?

```html
<style>
  section {
    width: 500px;
  }
  .box {
    width: 100%;
    padding: 20px;
    border: 4px solid;
    box-sizing: content-box;
  }
</style>

<section>
  <div class="box"></div>
</section>
```
</div>

`548px x 48px`

Because the `.box` has `box-sizing: content-box` width refers to the box content and padding and border are added on top.

<div markdown="block" data-question>

## What are the dimensions of the box in the following example?

```html
<style>
  section {
    width: 500px;
  }
  .box {
    width: 100%;
    padding: 20px;
    border: 4px solid;
    box-sizing: border-box;
  }
</style>

<section>
  <div class="box"></div>
</section>
```
</div>

`500px x 48px`

Because the `.box` has `box-sizing: border-box` width refers to the box content including padding and border.

## In css can borders or padding have negative values?

No

## In css can margins have negative values?

Yes

## In css how do you apply a margin that seeks to fill the maximum available space?

Using `margin: auto`

## In css how do you use margin to center an element?

Apply `margin-left: auto; margin-right: auto;` Both margins will seek to fill the maximum available space.

## Can you give a width or height to an inline element in flow layout?

No


## Can you assign a margin left or margin right to an inline element in flow layout?

Yes

## In flow layout if two block elements have enough space to render side by side do they render side by side or do they stack vertically?

They stack vertically

## What causes extra space around inline elements if their padding, border, and margin are set to 0?

`line-height`

Inline elements are assumed to be typography and are granted extra space based on the `line-height` property.

<div markdown="block" data-question>
## What css property can be used to apply padding to each line of an inline element?

The default behavior

![](default-padding-behavior.png)

The desired behavior

![](desired-padding-behavior.png)
</div>


`box-decoration-break: clone;`
## What is the default value of the css property `box-decoration-break`?

`slice`

## What is the main limitation of an `inline-block` element?

The inline block element cannot line-wrap.

## What is the difference between `width:auto` and `width:100%` in css?

Width auto fills the available space. Width 100% sets the width to the size of the parent element's content box.

## What does `width: min-content` do in css?

Make the element become as small as it can based on the child contents.

## What is the difference between an intrinsic and extrinsic value in css?

Intrinsic values are based on an element or an element's contents. Extrinsic values are based on an element's parent.

## Is `width: auto` an intrinsic or extrinsic value?

`extrinsic` -- width auto specifies that the width should dynamically fill the space *available in the parent element*.


## Is `width: min-content` an intrinsic or extrinsic value?

`intrinsic` -- min-content specifies that the width should collapse to as small as possible *based on the child contents*.

## What does `width: max-content` do in css?

Set the width to the smallest value that contains the content without line breaks even if this value is larger than the parent width.

## Is `width: max-content` an intrinsic or extrinsic value?

`intrinsic` -- max-content specifies that the width should expand to the point that there are no line breaks in the content even if this means expanding beyond the width of the parent.

## How does `width: fit-content` work in css?

If the width of the element's children is less than the width of the parent the width behaves like `width: max-content` and the width shrinks to the size of the content. If the width is larger than the available space in the parent the width adds line breaks to ensure it never exceeds the available space similar to `width: auto`

![](fit-content-width-example.png)

## How do width, min-width, and max-width interact in css?

The values are prioritized `min-width`, `max-width`, `width`.

If `max-width` is less than `min-width` then the element will use `min-width`.

<div markdown="block" data-question>

## Fill in the blanks in the algorithm css uses to calculate the width of an element


1. The browser calculates the width based on the {{c1::width}} value, ignoring {{c1::min-width}} and {{c1::max-width}}
2. If width is greater than max-width the browser recalculates width based on the {{c2::max-width}} value, ignoring {{c2::min-width}} and {{c2::width}}
3. If width is greater than min-width the browser recalculates width based on the {{c3::min-width}} value, ignoring {{c3::width}} and {{c3::max-width}}

</div>

## How can you replicate `width: fit-content` in IE11?

`display: table`

Display table causes an element to shrink to the size of it's contents but the element is still a block level element.

## What is the default height for an element in flow layout in css?

The element's height will shrink to the minimum height necessary to fit the element's content.


<div markdown="block" data-question>
## Why does height 100% on the following element not work?


```html
<style>
.wrapper {
  height: 100%;
}
</style>

<html>
<body>
<div class="wrapper">
</div>
</body>
</html>
```
</div>

Because the percentage height is based on the parent height and `body` does not have a height set which means it defaults to shrinking to contain it's children.

<div markdown="block" data-question>
## How can we make the div in the following example fill the entire page while allowing for the content to expand beyond the page height if necessary?


```html
<style>
.wrapper {
  height: 100%;
}
</style>

<html>
<body>
<div class="wrapper">
</div>
</body>
</html>
```
</div>

Add `height:100%` to `html` and `body` and `height: 100%` to `min-height: 100%` on the wrapper.

```html
<style>

html, body {
  height: 100%;
}

.wrapper {
  min-height: 100%;
}
</style>
```

When html has `height: 100%` it takes up the height of the viewport. The body will expand to fill the size of `html` and the `.wrapper` will expand to fill the size of `body` but grow larger than the body if the content fills more than a page.


