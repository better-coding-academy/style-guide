# Better Coding Academy Style Guide

## What is this?

This is a non-exhaustive set of coding principles you are expected to follow whilst studying at Better Coding Academy.

I personally follow this style guide for all production code that I write, so feel free to use it / extend from it in any of your production projects as well.

## Why use a style guide?

Having a consistent coding style across your projects is one of the easiest ways to keep coding quality and interoperability high. Learning to be consistent and follow the style guide of a company (hopefully they have one) pays handsome dividends.

## General Rules

### Indentation

**No tabs.** Instead, tabs should be remapped to insert two spaces. Tabs are not consistently rendered across programs and operating systems, sometimes having a width of 4, and sometimes even a width of 8, which is why using spaces that appear like tabs works best.

## HTML

### Tags

All tag names must be valid HTML tags (unless otherwise supported through the use of custom HTML elements).

```html
<!-- good -->
<h1>Hello</h1>
<p>I am a paragraph</p>

<!-- bad -->
<cool-heading>Yo</cool-heading>
```

All tag names must strictly be lowercase.

```html
<!-- good -->
<h1>Hello</h1>
<p>I am a paragraph</p>

<!-- bad -->
<H1>Hello</H1>
<P>I am a paragraph</p>
```

All self-closing tags must have a space and `/>` after all attributes.

```html
<!-- good -->
<img src="image.jpg" />
<br />

<!-- bad -->
<img src="image.jpg">
<img src="image.jpg"></img>
<img src="image.jpg"/>
```

Non-self-closing tags must **not** self-close.

```html
<!-- good -->
<p>Hello</p>

<!-- bad -->
<p />
```

### Attributes

All attributes must strictly be in alphabetical order.

```html
<!-- good -->
<input placeholder="Username" size="10" type="text" value="foo" />

<!-- bad -->
<input type="text" placeholder="Username" value="foo" size="10" />
```

All attributes must be valid HTML attributes in their valid lowercase form, or otherwise be preceded by `data-`.

```html
<!-- good -->
<img data-image-for="myPage" src="image.jpg" />
<button onclick="doSomething();">Click Me</button>

<!-- bad -->
<img image-for="myPage" src="image.jpg" />
<button onClick="doSomething();">Click Me</button>
```

## CSS

### Selectors

Don't use anything other than class names and tag names for selecting.

Class name selectors must use kebab-case.

**What about IDs?** IDs are reserved for selection purposes in JavaScript.

**What about attributes?** They're allowed, but only in tandem with an appropriate tag name. For example:

```css
/* good */
input[type="text"] {
  font-weight: bold;
}

/* bad */
[type="text"] {
  font-weight: bold;
}
```

The value in an attribute selector must be surrounded by double quotes.

```css
/* good */
input[type="text"] {
  font-weight: bold;
}

/* bad */
input[type=text] {
  font-weight: bold;
}
```

### Declaration Blocks

The formatting must be as follows:

```css
<selector> {
  /* two spaces from the left */
  <declarations>
}
```

Every declaration block must be separated from other blocks (and `@import` statements) by a new line.

```css
/* good */
@import url("https://fonts.googleapis.com/css?family=Roboto&display=swap");

body {
  font-family: Roboto, sans-serif;
}

.body {
  font-weight: bold;
}

/* bad */
@import url("https://fonts.googleapis.com/css?family=Roboto&display=swap");
body {
  font-family: Roboto, sans-serif;
}
.body {
  font-weight: bold;
}
```

Tag-based declaration blocks go first, and then class names.

```css
/* good */
body {
  font-family: Arial, Helvetica, sans-serif;
}

.bold {
  font-weight: bold;
}

/* bad */
.bold {
  font-weight: bold;
}

body {
  font-family: Arial, Helvetica, sans-serif;
}
```

### Declarations

Declarations must be in alphabetical order.

```css
/* good */
.square {
  background-color: red;
  height: 100%;
  width: 100px;
}

/* bad */
.square {
  width: 100px;
  height: 100%;
  background-color: red;
}
```

Where possible, try not to use vendor prefixes; instead use a CSS preprocessor to add them for you where possible. However, if you were to add vendor prefixes, add them prior to their associated property, in alphabetical order.

```css
/* good */
.custom-select {
  -moz-appearance: none;
  -webkit-appearance: none;
  appearance: none;
  background-color: green;
  -moz-border-radius: 5px;
  -webkit-border-radius: 5px;
  border-radius: 5px;
}
```

If you are using a vendor prefix without the "normal" version of the declaration, put it where it would belong if it did not have the vendor prefix.

```css
/* good */
.funky-text {
  -webkit-background-clip: text; /* "clip" before "image" */
  background-image: url(image.jpg);
  -webkit-text-fill-color: transparent;  /* "text" after "back" */
}
```