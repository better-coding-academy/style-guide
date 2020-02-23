<!-- omit in toc -->
# Better Coding Academy Style Guide

<!-- omit in toc -->
## What is this?

This is a non-exhaustive set of coding principles you are expected to follow whilst studying at Better Coding Academy.

I personally follow this style guide for all production code that I write, so feel free to use it / extend from it in any of your production projects as well.

<!-- omit in toc -->
## Why use a style guide?

Having a consistent coding style across your projects is one of the easiest ways to keep coding quality and interoperability high. Learning to be consistent and follow the style guide of a company (hopefully they have one) pays handsome dividends.

<!-- omit in toc -->
## Table of Contents

- [General Rules](#general-rules)
  - [Indentation](#indentation)
  - [Quotes](#quotes)
- [HTML](#html)
  - [Tags](#tags)
  - [Attributes](#attributes)
- [CSS](#css)
  - [Selectors](#selectors)
  - [Declaration Blocks](#declaration-blocks)
  - [Declarations](#declarations)
  - [Miscellaneous](#miscellaneous)
- [JavaScript](#javascript)
  - [Variables](#variables)
  - [Functions](#functions)
  - [Quotes](#quotes-1)
  - [Spacing](#spacing)
  - [Loops](#loops)

## General Rules

### Indentation

**No tabs.** Instead, tabs should be remapped to insert two spaces. Tabs are not consistently rendered across programs and operating systems, sometimes having a width of 4, and sometimes even a width of 8, which is why using spaces that appear like tabs works best.

### Quotes

**Use double quotes.**

**Are there situations in which using single quotes is appropriate?** Yes, absolutely. See below under the [JavaScript](#javascript) heading for more information.

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

### Miscellaneous

**Try not to use `!important`.** `!important` is needed in only a very small percentage of use cases. In most other cases, simply reordering your CSS declarations can do the trick. CSS declarations of the same specificity level are applied in a top-down fashion, so if you want a style to take precedence, simply try moving it further down instead of using `!important`.

**Try not to use `z-index`.** Instead of using `z-index`, in the large majority of cases you can simply reorder elements. For example:

```html
<style>
  .square {
    position: absolute;
  }
</style>

<div class="square">square 1</div>
<div class="square">square 2</div>
<div class="square">square 3</div>
<div class="square">square 4</div>
```

Square 4 will naturally be on top of Square 3, which will be on top of Square 2, and so on.

## JavaScript

### Variables

**Never use `var`.** This ensures that you can’t reassign your references, which can lead to bugs and difficult to comprehend code.

```js
// good
const number = 5;

// bad
var number = 5;
```

**Use `let` only where absolutely necessary.** Just like with `var`, this prevents unnecessary assignments.

```js
// good
const number = 5;
let someComplexValue;
if (condition) {
  doSomething();
  doSomethingElse();
  someComplexValue = doAnotherThing();
} else {
  doSomethingElse();
  someComplexValue = doSomething();
}

// bad
let number = 5;
```

### Functions

Use arrow functions where possible. Use the `function` keyword only when you need the `this` value.

**Why?** Arrow functions are shorter and give a more intuitive understanding of `this`. `this` should be reserved for use in specific situations instead of having every function have its own "accidental" `this` value.

```js
// good
const add = (num1, num2) => num1 + num2;

const handleSubmit = async ({ name }) => {
  const result = await addUser({ variables: { name }});
  return result.data;
}

input.addEventListener("keydown", function (evt) { 
  evt.preventDefault();

  alert(`Hello ${this.value}!`);
});

// bad
function add(num1, num2) {
  return nume + num2;
}

async function handleSubmit({ name }) {
  const result = await addUser({ variables: { name }});
  return result.data;
}
```

### Quotes

Use double quotes `""` for strings.

```js
// good
const message = "Hello!";

// bad
const message = 'Hello!';
```

However, if you wish to embed double quotes in your string, you can use single quotes or backticks - avoid escaping where possible.

```js
// good
const message = 'And then he said "Hello", like a maniac!';
const message = `And then he said "Hello", like a maniac!`;

// bad
const message = "And then he said \"Hello\", like a maniac!";
```

Use backticks whenever you need to interpolate a value into your string.

```js
// bad
console.log("How are you, " + name + "?");
console.log(["How are you, ", name, "?"].join());

// good
console.log(`How are you, ${name}?`);
```

### Spacing

Put one new line before and after every function in your code (unless there's no code before/after it).

```js
// good
function func1() {
  // something
}

function func2() {
  // something else
}

// bad
function func1() {
  // something
}
function func2() {
  // something else
}
```

Put one new line before and after every method and property in your class (unless it's at the start/end of your class).

```js
// good
class Form extends Component {
  state = { a: 1, b: 2 };

  handleChange = () => {
    // ...
  }

  render() {
    // ...
  }
}

// bad
class Form extends Component {
  state = { a: 1, b: 2 };
  handleChange = () => {
    // ...
  }
  render() {
    // ...
  }
}
```

### Loops

Try not to use `for` loops where possible.

Instead, consider using Array iteration methods, e.g. `Array.prototype.forEach` or `Array.prototype.map`.

```js
const names = ["Aaron", "Amanda", "Arthur"];

// good
names.forEach(name => {
  console.log(name);
})

const namesInCaps = names.map(name => name.toUpperCase());

// bad
for (let i = 0; i < names.length; i++) {
  console.log(name);  
}
```

However, there are some cases in which you will need to use `for` loops. In such cases, you should use a proper counter name (not `i`).