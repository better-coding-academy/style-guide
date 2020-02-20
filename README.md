# Better Coding Academy Style Guide

## What is this?

This is a non-exhaustive set of coding principles you are expected to follow whilst studying at Better Coding Academy.

I personally follow this style guide for all production code that I write, so feel free to use it / extend from it in any of your production projects as well.

## Why use a style guide?

Having a consistent coding style across your projects is one of the easiest ways to keep coding quality and interoperability high. Learning to be consistent and follow the style guide of a company (hopefully they have one) pays handsome dividends.

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

<!-- good -->
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

More to come! Stay tuned 😎