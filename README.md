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
  - [Editor](#editor)
  - [Formatter](#formatter)
- [HTML](#html)
  - [Tags](#tags)
  - [Attributes](#attributes)
- [CSS](#css)
  - [Selectors](#selectors)
  - [Declaration Blocks](#declaration-blocks)
  - [Declarations](#declarations)
  - [Miscellaneous](#miscellaneous)
- [JavaScript](#javascript)
  - [Semicolons](#semicolons)
  - [Variables](#variables)
  - [Objects](#objects)
  - [Functions](#functions)
  - [Quotes](#quotes-1)
  - [Spacing](#spacing)
  - [Loops](#loops)
  - [Switch Statements](#switch-statements)
  - [DOM Operations](#dom-operations)
  - [Comments](#comments)
  - [Miscellaneous](#miscellaneous-1)
- [React](#react)
  - [Component Types](#component-types)
  - [Props](#props)
  - [Architecture](#architecture)
- [Performance](#performance)

## General Rules

### Indentation

**No tabs.** Instead, tabs should be remapped to insert two spaces. Tabs are not consistently rendered across programs and operating systems, sometimes having a width of 4, and sometimes even a width of 8, which is why using spaces that appear like tabs works best.

### Quotes

**Use double quotes.**

**Are there situations in which using single quotes is appropriate?** Yes, absolutely. See below under the [JavaScript](#javascript) heading for more information.

### Editor

It is suggested that you use VSCode for writing code.

**Why?** Well, as a non-exhaustive list, VSCode:

1. Supports a multiitude of extensions;
2. Has great customisability and extensibility;
3. Supports WSL (Windows Subsystem for Linux); and
4. Is faster than Atom (which used to be my editor of choice).

### Formatter

The use of [Prettier](https://prettier.io/) is **highly recommended**, as it would help automatically enforce a number of the rules presented within this document.

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

**Try not to use inline styles.** Unless applied using JavaScript for dynamic property values (e.g. `transform`, `left`, `top`, etc.), there's probably no good reason to use inline styles.

**But if I don't use inline styles, then the styles don't work!** That's a specificity issue. You probably have other styles applied at too high a specificity (e.g. using `!important`, which is a no-no as well 😉) overriding your normal styles. In this case, inline styles is like a band-aid over a stab wound - you need to dig deeper and investigate further to find the true source of the issue.

## JavaScript

### Semicolons

Wherever semicolons are optional, they should be included.

**Why?** Not having semicolons makes the code very trippy. For example, the following:

```js
// bad
function returnThree() {
  return
    3;
}
```

Returns:

```js
returnThree(); // undefined????
```

This is because JavaScript uses a set of rules called [Automatic Semicolon Insertion](https://tc39.github.io/ecma262/#sec-automatic-semicolon-insertion) to determine whether or not it should regard that line break as the end of a statement, and it decides where it wants to place semicolons into your code. As can be seen from the example above, ASI can definitely be somewhat counter-intuitive; hence why we recommend to explicitly terminate your statements and configure your linter to catch missing semicolons.

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

### Objects

Objects must have a curly brace on the first line, and either all properties on the same line, or one property on each line after the curly brace.

```js
// good
const factory = { name: "Willy Wonka" };
const person = {
  age: "unknown",
  name: "Willy Wonka",
  occupation: "chocolatier"
};

// bad
const factory = 
{
  name: "Wonka Willy"
};
const person = {
  age: "unknown", name: "Wonka Willy",
  occupation: "choco-late more like vanilla-early"
};
```

All object properties must be in alphabetical order.

```js
// good
const bill = {
  age: 25,
  email: "bill@example.com",
  name: "Bill"
}

// bad
const bill = {
  name: "Bill",
  age: 25,
  email: "bill@example.com"
};
```

**Why?** It doesn't make much of a difference for smaller objects; however, when you end up with more properties, such as in the following example:

```js
const options = {
  autoFocus: true,
  disabled: isSubmitting && isValid,
  displaySize: "lg",
  id: generateId("email"),
  name: "email",
  placeholder: "e.g. lucas@example.com",
  type: "text"
};
```

Assuming you know your alphabet, locating a property is simply a matter of binary search, i.e. O(log n). However, if we were to let the programmer do "whatever order feels right for them at the time", then we would get something like:

```js
const options = {
  id: generateId("email"),
  name: "email",
  displaySize: "lg",
  type: "text",
  placeholder: "e.g. lucas@example.com",
  autoFocus: true,
  disabled: isSubmitting && isValid
};
```

As it becomes harder to read, some programmers would then start adding pointless new lines, grouping once again "as they see fit":

```js
const options = {
  // no one
  id: generateId("email"),
  name: "email",

  // has any idea
  displaySize: "lg",
  type: "text",

  // why these are grouped like this
  placeholder: "e.g. lucas@example.com",
  autoFocus: true,
  disabled: isSubmitting && isValid
};
```

So yeah, no good. Finding a property in an unordered object is O(n), an order of magnitude worse than O(log n).

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

When definining the parameters of a function/method, **one object parameter is generally preferable to multiple arguments**.

For example, instead of this:

```js
// bad
class User {
  constructor(id, name, email, address) {
    this.id = id;
    this.name = name;
    this.email = email;
    this.address = address;
  }
}
```

Do this:

```js
// good
class User {
  constructor({ address, email, id, name }) {
    this.id = id;
    this.name = name;
    this.email = email;
    this.address = address;
  }
}
```

This has three main benefits:

1. **It easily allows for properties to be optional.** Imagine if `email` were to be optional; creating an object using the first syntax would look like:

    ```js
    new User(1, "Lucas", undefined, "1 Main St.");
    ```

    However, for the second one it would simply be:

    ```js
    new User({
      address: "1 Main St.",
      // notice how we leave out email entirely
      id: 1,
      name: "Lucas"
    });
    ```

2. **It removes the ambiguity of ordering.** In the first example, there is no real reason to use the order `id, name, email, address` as opposed to, say, `id, name, address, email`, or any other combination really. When using an object and destructuring it, it is easier than remembering an arbitrary order.
3. **It gives each "argument" a name.** Obviously in the second example we only have one argument (an object); however, each one of those properties has a name, which adds incredible semantics into your funciton. Look at the difference between these two:

    ```php
    // actual PHP code... yikes
    $canvas = imagecreatetruecolor(200, 200);

    // yikes
    $pink = imagecolorallocate($canvas, 255, 105, 180);
    $white = imagecolorallocate($canvas, 255, 255, 255);
    $green = imagecolorallocate($canvas, 132, 135, 28);

    // yikes
    imagerectangle($canvas, 50, 50, 150, 150, $pink);
    imagerectangle($canvas, 45, 60, 120, 100, $white);
    imagerectangle($canvas, 100, 120, 75, 160, $green);
    ```

    Using what we've just learned, what if we rewrite this a little?

    ```js
    const canvas = imageCreateTrueColor({ height: 200, width: 200 });

    const pink = imageColorAllocate({
      blue: 180,
      canvas,
      green: 105,
      red: 255
    });
    const white = imageColorAllocate({
      blue: 255,
      canvas,
      green: 255,
      red: 255
    });
    const green = imageColorAllocate({
      blue: 28,
      canvas,
      green: 135,
      red: 132
    });

    imageRectangle({
      canvas,
      color: pink,
      x1: 50,
      x2: 150,
      y1: 50,
      y2: 150
    });
    imageRectangle({
      canvas,
      color: white,
      x1: 45,
      x2: 120,
      y1: 60,
      y2: 100
    });
    imageRectangle({
      canvas,
      color: green,
      x1: 100,
      x2: 75,
      y1: 120,
      y2: 160
    });
    ```

    Yes, it is longer; however, look at all the additional information that is now available. No need to remember the order of parameters, and that is a huge deal. It might take 20% longer to type the first time round, but each time a change is made, the reduction in amiguity will save much more than the original 20% cost.

**Do not mutate function arguments.** Instead, if the argument is a primitive, consider storing its value in a new object; if the argument is an object (including arrays), consider spreading it or otherwise creating a new copy.

```js
// bad
const magickFruits = numFruits => {
  numFruits *= 2;
  
  // etc.
}

// good
const magickFruits = numFruits => {
  let newNumFruits = numFruits * 2;

  // etc.
}
```

**Why?** If the argument is a primitive, once you change its value, you no longer have access to the original value within the scope of the function. Any code that you write later on in the function that might rely on the argument will now no longer be able to access the original value. If the argument is an object, you are mutating its original value, which introduces side effects into the rest of your code - and is even worse. For example:

```js
// bad
const append1 = array => {
  array.push(1);
  return [...array];
}

const arr = [1, 2, 3, 4, 5];
const newArr = append1(arr);

arr; // [1, 2, 3, 4, 5, 6]
newArr; // [1, 2, 3, 4, 5, 6]

// good
const append1 = array => {
  const newArray = [...array, 1];
  return newArray;
}

const arr = [1, 2, 3, 4, 5];
const newArr = append1(arr);

arr; // [1, 2, 3, 4, 5]
newArr; // [1, 2, 3, 4, 5, 6]
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

Try not to use `for` loops where possible. Instead, consider using Array iteration methods, e.g. `Array.prototype.forEach` or `Array.prototype.map`.

**Why?** Specificity and clarity. When you see a `.map` method, assuming no crazy stuff is going on, you know that a new array is being generated from an existing array. When you see a `.forEach` method, you know that it is iterating thorugh properties, and so on and so forth for `.reduce`, `.some`, `.every`, etc. - every single method is clearly defined for a particular purpose.

However when you see a `for` loop, there is no guarantee for what is going to happen, and in many cases, when it tries to do more than one thing, the loop quickly becomes overcomplicated and poorly designed.

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

However, there are some cases in which you will need to use `for` loops. In such cases, you should use a proper counter name (not `i`) where possible. However, using a generic name like `i` is okay if you are only repeating something a certain number of times, and do not plan to use the index for any purposes.

### Switch Statements

Try to use `switch` statements as little as possible.

**Why?** They're essentially `if` statements that sacrifice flexibility for a little bit more minimalism (and even that is debatable).

For example, look at the following code:

```js
const status = "GO";
switch (status) {
  case "GO":
    console.log("Let's go!");
    break;
  case "STOP":
    console.log("Time to stop!");
    break;
}
```

And its equivalent using `if` statements:

```js
const status = "GO";
if (status === "GO") {
  console.log("Let's go!");
} else if (status === "STOP") {
  console.log("Time to stop!");
}
```

I mean... it's 3 lines shorter - I guess the only thing is that `status` is not repeated. However, going back to the `switch` statement, what if you want to have some more granular control?

```js
const status = "GO";
const car = "RACECAR";
switch (status) {
  case "GO":
    console.log("Let's go!");
    break;
  case "STOP":
    // yikes
    if (car === "RACECAR") {
      console.log("Let's GO!");
    } else {
      console.log("Time to stop!");
    }
    break;
}
```

Compared to if we were using `if` statements:

```js
const status = "GO";
const car = "RACECAR";
if (status === "GO") {
  console.log("Let's go!");
} else if (status === "STOP" && car === "RACECAR") {
  console.log("Let's GO!");
} else if (status === "STOP") {
  console.log("Time to stop!");
}
```

**Are there cases in which using a switch statement is appropriate?** Sure! Well, maybe... I don't know. At the lowest level it's a matter of personal preference; however, hopefully you can see why I do not advocate its widespread use.

### DOM Operations

Try to update the DOM as little as possible.

**Why?** Updating the DOM is "slow". Slow, as in relatively slow compared to updating internal JavaScript variables. In other words:

```js
someHTMLElement.innerText = "Hello"; // this
someVariable = "Hello";              // is slower than this
```

Compare the following two bits of code that do essentially the same thing:

```js
const preTag = document.createElement("pre");
document.body.appendChild(preTag);

// bad
for (let i = 0; i < 100; i++) {
  preTag.innerText += `${Math.random()}\n`; // in total, 100 DOM update operations
}

// good
let preTagContents = preTag.innerText; // store the value (DOM access operation)
for (let i = 0; i < 100; i++) {
  preTagContents += `${Math.random()}\n`; // update the variable - much faster...
}
preTag.innerText = preTagContents; // and write it into the DOM! (a single DOM update operation)
```

[Check out this JSPerf test to run both of these snippets on your own computer.](https://jsperf.com/dom-access-speed/1)

**Do not read style properties to determine information about your page.** Take a look at the following code, designed to increase the font size of an element by 1px:

```js
// headingEl already exists

// bad
headingEl.style.fontSize = `${parseInt(headingEl.style.fontSize) + 1}px`;
```

**Why?** Disregarding whether this works or not (and in some't cases it won't work) this is an anti-pattern because we're depending on data that is stored within the DOM.

Instead, do something like:

```js
// headingEl already exists

const DEFAULT_HEADING_FONT_SIZE = 16;
let headingFontSize = DEFAULT_HEADING_FONT_SIZE; // pre-set this

// good
headingEl.style.fontSize = `${++headingFontSize}px`; // adds 1 and then inlines it
```

This way our `headingFontSize` variable (i.e. our JavaScript) is the source of truth for the data - much cleaner, no `parseInt` required.

**Do not store data on the DOM.** Instead, store your data inside your JavaScript code, whether that is in the form of single variables, objects, arrays, etc.

**Why?** The DOM the presentational layer, not the data layer. Storing data on the DOM only to be accessed by your own JavaScript code results in a new **source of truth** (i.e. the DOM, where the data is stored). This only leads to issues further down the track.

```js
/* bad */
someElement.isValid = false;

// later on in the code...
if (!someElement.isValid) {
  // ...
}

/* good */
let isSomeElementValid = false;

// later on in the code
if (!isSomeElementValid) {
  // ...
}
```

### Comments

**Don't comment anything that is already obvious in your code.**

The following is an example of how **NOT** to comment:

```js
// Hook
function useLocalStorage(key, initialValue) {
  // State to store our value
  // Pass initial state function to useState so logic is only executed once
  const [storedValue, setStoredValue] = useState(() => {
    try {
      // Get from local storage by key
      const item = window.localStorage.getItem(key);
      // Parse stored json or if none return initialValue
      return item ? JSON.parse(item) : initialValue;
    } catch (error) {
      // If error also return initialValue
      console.log(error);
      return initialValue;
    }
  });
```

None of the comments shown above provide any additional information to the given code - all of that information can be inferred from the code. In comaprison, the following is an example of a good comment:

```js
module.exports = {
  env: {
    browser: true,
    es6: true, // gets Promise working
    jest: true,
    node: true
  },
```

In comparison, the one comment here for `es6: true` tells us what we otherwise could not have inferred. This above snippet is from a `.eslintrc.js` file, and `es6: true` does more than just get `Promise` working - however, we're writing this comment to explain why this is being done in this particular case; that is, to get `Promise` working.

### Miscellaneous

**Avoid magic numbers.** Magic numbers are unique values with unexplained meaning or multiple occurrences which could (preferably) be replaced with one or more named constants.

Let's look at the following example:

```js
const square = document.createElement("div");
square.style.width = "100px";
square.style.height = "100px";
square.style.position = "absolute";
square.style.left = "100px";
square.style.top = "100px";
```

In the above, the `100px` shown on the four lines are the magic numbers. Specifically, they refer to values whose origins are unclear, and are not clearly explained.

You might not be able to see why the above example is bad; however, what if we continued using this `square`?

```js
// some sort of collision detection...
const squareRect = square.getBoundingClientRect();
if (
  squareRect.left <= collisionRect.left &&
  squareRect.left + 100 >= collisionRect.left &&
  squareRect.top <= collisionRect.top &&
  squareRect.top + 100 >= collisionRect.top
) {
  // etc...
}
```

All of a sudden the number `100` starts appearing all over your code, and for no real reason! Changing it in any location will break something, but the longer you leave it there, the less clear its purpose becomes.

Instead, stem it from the beginning with a variable:

```js
const SQUARE_SIZE = 100;
const SQUARE_DEFAULT_LEFT = 100;
const SQUARE_DEFAULT_TOP = 100;

const square = document.createElement("div");
square.style.width = `${SQUARE_SIZE}px`;
square.style.height = `${SQUARE_SIZE}px`;
square.style.position = "absolute";
square.style.left = `${SQUARE_DEFAULT_LEFT}px`;
square.style.top = `${SQUARE_DEFAULT_TOP}px`;
```

Notice the UPPER_SNAKE_CASING that we use for these constants. Because they're values that are pre-defined by the programmer and hence cannot be customised, we use this casing.

Notice how we used a different constant for `left` and for `top`. This is to prevent confusion as to why the left and top values are being set to the square size. If you wish the left and top values to be related to the square size, you could do:

```js
const SQUARE_SIZE = 100;
const SQUARE_DEFAULT_LEFT = SQUARE_SIZE;
const SQUARE_DEFAULT_TOP = SQUARE_SIZE;
```

This is a good compromise to semantically show that `SQUARE_DEFAULT_LEFT` and `SQUARE_DEFAULT_TOP` are both based off `SQUARE_SIZE`.

## React

### Component Types

**Use function-based components wherever possible, and class-based components only when absolutely necessary.** "Absolutely necessary" includes, as a very limited list:

1. [Error boundaries that use `componentDidCatch`](https://reactjs.org/docs/error-boundaries.html); and
2. Components that **need** a class-based structure to work properly / be properly optimised. Expanding upon this, this does **not** mean that you get to arbitrarily decide when to use class-based components based on a "gut feeling" - you **must** look at hard data for evidence that using a class-based component provides a statistically significant optimisation benefit. See [Performance](#performance) below.

### Props

**All props should be in alphabetical order.**

```jsx
// good
<input name="email" placeholder="e.g. lucas@example.com" required type="email" />

// bad
<input type="email" required name="email" placeholder="e.g. lucas@example.com" />
```

**Event handler props should be named in the convention of `onAction`.**

```jsx
// good
<CreateAccount
  onCreate={() => {
    // ...
  }}
  onUpdate={() => {
    // ...
  }}
/>

// bad
<CreateAccount
  create={() => {
    // ...
  }}
  updated={() => {
    // ...
  }}
/>
```

**Why?** React does this with all of its built-in events. It is important to discern between normal props and event handler props, so we might as well follow React's convention.

**When accessing event handler props inside your component, they should be remapped to use the word "push".**

```jsx
// good
const CreateAccount = ({ onCreate: pushCreate, onUpdate: pushUpdate }) => {
  // later on...
  pushCreate({ ... });
}

// bad
const CreateAccount = ({ onCreate, onUpdate }) => {
  // later on...
  onCreate({ ... });
}
```

**Why?** A function called `onEventName` doesn't make much sense - `pushEventName` makes a lot more sense.

### Architecture

**When deciding between hooks, render props and higher-order components, always go with hooks wherever possible.**

```jsx
// #1
const MyComponent = () => {
  const mousePosition = useMouse();

  // mousePosition.x, mousePosition.y
}

// #2
const MyComponent = () => {
  return (
    <Mouse>
      {({ x, y }) => {
        // ...
      }}
    </Mouse>
  )
}

// #3
const MyComponent = ({ x, y }) => {
  // ...
}

export default withMouse(MyComponent);
```

**Why?** Well, let's start with higher-order components.

Higher order components are bad for two main reasons:

1. **They take up a fixed prop name, possibly removing other props.** For example, imagine for above example #3 we want to include an `x` and `y` prop on the component:

    ```jsx
    <MyComponent x="some value" y="some other value" />
    ```

    Both of these values will be overwritten by the values coming from the higher order component. This issue can also arise when you wish to use multiple higher order components:

    ```jsx
    export default withMouse(withPage(MyComponent)); // if withMouse and withPage set the same props, there will be clashing issues
    ```

2. **They do not clearly identify the source of your data.** `withMouse(MyComponent)` does not tell you which props are being included onto the component (if any), hence increasing the amount of time spent debugging and fixing up the code.

Okay then, now let's look at **render props**. Because render props give you data within a function parameter, you can freely rename it however you like. For example:

```jsx
<Mouse>
  {({ x, y }) => (
    <Page>
      {({ x: pageX, y: pageY }) => {
        // ^ big brain
      }}
    </Page>
  )}
</Mouse>
```

However, render props still have their own issues:

1. **They don't allow you to use their data outside of the `return` statement.** With the example above, you can't use the `x` and `y` values in any state variables, `useEffect` hooks, or any other functions within your component, because it's only accessible within the `return` statement.
2. **They get nested... really quickly.** Imagine we have three render prop components within a given component:

    ```jsx
    const MyComponent = () => {
      return (
        <Mouse>
          {({ x, y }) => (
            <Page>
              {({ x: pageX, y: pageY }) => (
                <Connection>
                  {({ api }) => {
                    // yikes
                  }}
                </Connection>
              )}
            </Page>
          )}
        </Mouse>
      )
    };
    ```

So now, onto the final (and best) solution!

Hooks address all of the above issues.

1. **Hooks don't have any fixed prop names** - you can rename however you like:

    ```jsx
    const { x, y } = useMouse();
    const { x: pageX, y: pageY } = usePage();
    ```

2. **Hooks clearly identify the source of the data** - in the example above, it's clear that `x` and `y` come from `useMouse`, and `pageX` and `pageY` come from `usePage`.
3. **Hooks allow you to access data outside of the `return` statement.** For example, you can do stuff like:

    ```jsx
    const { x: pageX, y: pageY } = usePage();

    useEffect(() => {
      // this runs whenever pageX or pageY changes
    }, [pageX, pageY]);
    ```

4. **Hooks don't get nested at all.** With the above render prop monstrosity rewritten using hooks, the code would look something like:

    ```jsx
    const { x, y } = useMouse();
    const { x: pageX, y: pageY } = usePage();
    const { api } = useConnection();
    ```

    Three lines of beautiful code.

## Performance

> “Premature optimization is the root of all evil." – Donald Knuth

What does this mean? Well, imagine you have a section of code like this:

```jsx
// good, not bad... but read on
const MyComponent = () => {
  useSomeHook();

  const handleClick = () => {
    alert("hello!");
  }

  return <button onClick={handleClick}>Click Me</button>;
};
```

You render this component onto your page, and everything is working fine.

However, you recently read an article published by an internet stranger, saying that this type of code is bad as `handleClick` gets re-defined every time `MyComponent` is run, which is bad for performance.

So, to get around this issue you decide to refactor this into a class-based component:

```jsx
// uh...
class MyComponent extends Component {
  handleClick = () => {
    alert("hello!");
  }

  render() {
    useSomeHook(); // uh oh...
    return <button onClick={this.handleClick}>Click Me</button>;
  }
}
```

OH wait... `useSomeHook` doesn't work anymore - we need to use functional components for that to work! Guess we'll have to rewrite that hook as well.

So now, because you tried to prematurely optimise `MyComponent`, not only have you introduced a class-based component, but you've also introduced a second, non-hook-based copy of `useSomeHook`, just so that you can get "performance benefits". However, instead of getting "performance benefits", you simply reduced your own efficiency as a developer.

**What happened?** Well, you didn't ask yourself the following questions:

1. **Is my code slow?** Yep. Is my code actually slow? Not like, "this seems bad so I'll change it" slow - is there a noticeable performance hit on my page?
2. **Is this section of code causing the performance hit?** In some cases it might be other sections of code. Unless you've done your research, it's very hard to tell. In the above example, we did not collect evidence showing that the `handleClick` method of `MyComponent` was causing a noticeable performance hit.
3. **Are the changes I'm proposing going to fix or mitigate the performance issue?** In the above example, we did not collect evidence showing that the use of a class-based component will noticeably increase the speed of `MyComponent` compared to a functional component.

Before you optimise yourself down a rabbit hole, always ask yourself the above questions, and make sure that you have good reasons to perform the optimisations you are about to do.

**So, does that mean we should never optimise?** No, of course not! Optimisation is very important; however, optimisation without data is just over-complication, and that is certainly not a good thing.