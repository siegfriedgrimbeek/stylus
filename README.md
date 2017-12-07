# Eeleven Stylus Styleguide

Stylus Naming Conventions and Style Guide();

Inspired by the [Airbnb CSS / Sass Styleguide](https://github.com/airbnb/css)

Official Stylus documentation: http://stylus-lang.com/docs/

Stylus Playground:
http://stylus-lang.com/try.html

Practise Project:
https://github.com/siegfriedgrimbeek/stylus-training

## Table of Contents

1. [Terminology](#terminology)
    - [Rule Declaration](#rule-declaration)
    - [Selectors](#selectors)
    - [Properties](#properties)

2. [General](#general)
    - [Folder Structure](#folder-structure)
    - [Naming Conventions](#naming-conventions)

3. [Stylus](#stylus)
    - [Formatting](#formatting)
    - [ID Selectors](#id-selectors)
    - [JavaScript hooks](#javascript-hooks)
    - [Nested Selectors](#nested-selectors)
    - [Ordering](#ordering-of-property-declarations)
    - [Variables](#variables)
    - [Mixins](#mixins)
    - [Code Example](#code-example)


## Terminology

### Rule declaration

A “rule declaration” is the name given to a selector (or a group of selectors) with an accompanying group of properties. Here's an example:

```scss
.listing
  font-size: 18px
  line-height: 1.2
```

### Selectors

In a rule declaration, “selectors” are the bits that determine which elements in the DOM tree will be styled by the defined properties. Selectors can match HTML elements, as well as an element's class, ID, or any of its attributes.

Here are some examples of selectors:

```scss
.my-element-class
  /* ... */

[aria-hidden]
  /* ... */

```

### Properties

Finally, properties are what give the selected elements of a rule declaration their style. Properties are key-value pairs, and a rule declaration can contain one or more property declarations.

Property declarations look like this:

```scss
/* some selector */
  background: #f1f1f1
  color: #333

```


**[⬆ back to top](#table-of-contents)**

## General

### Folder Structure
The folder structure of the stylus code should follow the folder structure of the components as closely as possible.

A user should not have to search for any code, it should either be in the component specific stylus file or in the mixins file.

```styl
./form
  |-- variables.styl
  |-- mixins.styl

./product
  |-- body.styl
  |-- form.styl
  |-- foot.styl
  |-- head.styl
```

### Naming Conventions

Clear and concise class names should be given to each element. If in doubt of naming, consult with the team to determine an acceptable name.

Use dashes over camelCase for class names.

File specific **variables** should be easily distinguished by using the underscore naming convention as per the [Variables](#variables) section.

**[⬆ back to top](#table-of-contents)**

## Stylus

### Formatting

* Use soft tabs (2 spaces) for indentation
* Use dashes over camelCase for class names
* Do not use ID selectors
* When using multiple selectors in a rule declaration, give each selector its own line.
* Use a single `:` character for a rule declaration
  - In properties, put a space after, but not before, the `:` character
* Do not follow a rule declaration up with a `;` character
* Put blank lines between rule declarations

**Bad**

```scss
.avatar
    border-radius:50%;
    border:2px solid white;
.no, .nope, .not_good
    border:2px solid white;

#lol-no
  border:2px solid white;

```

**Good**

```scss
.avatar
  border-radius: 50%
  border: 2px solid white

.one,
.selector,
.per-line
  border:2px solid white

```

### Comments

* Prefer line comments (`//`) to block comments
* Prefer comments on their own line. Avoid end-of-line comments
* Write detailed comments for code that isn't self-documenting:
  - Uses of z-index
  - Compatibility or browser-specific hacks


### ID selectors

While it is possible to select elements by ID in CSS, it should generally be considered an anti-pattern. ID selectors introduce an unnecessarily high level of [specificity](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity) to your rule declarations, and they are not reusable.

For more on this subject, read [CSS Wizardry's article](http://csswizardry.com/2014/07/hacks-for-dealing-with-specificity/) on dealing with specificity.

### JavaScript hooks

Avoid binding to the same class in both your CSS and JavaScript. Conflating the two often leads to, at a minimum, time wasted during refactoring when a developer must cross-reference each class they are changing, and at its worst, developers being afraid to make changes for fear of breaking functionality.

We recommend creating JavaScript-specific classes to bind to, prefixed with `.js-`:

```html
<button class="btn btn-primary js-request-to-book">Request to Book</button>
```

### Nested selectors

**Do not nest selectors more than three levels deep!**

```scss
.page-container
  .content
    .profile
      // STOP!
```

When selectors become this long, you're likely writing CSS that is:
  * Strongly coupled to the HTML (fragile) *—OR—*
  * Overly specific (powerful) *—OR—*
  * Not reusable

Again: **never nest ID selectors!**

If you must use an ID selector in the first place (and you should really try not to), they should never be nested. If you find yourself doing this, you need to revisit your markup, or figure out why such strong specificity is needed. If you are writing well formed HTML and CSS, you should **never** need to do this.

### Ordering of property declarations

1. Property declarations

    List all standard property declarations **first**, that is anything that isn't an `@include` or a nested selector.

    ```scss
    .btn-green
      background: green
      font-weight: bold
    ```

2. **Mixin** declarations

    Grouping **Mixins** at the end makes it easier to read the entire selector.

    ```scss
    .btn-green
      background: green
      font-weight: bold
      transition(background 0.5s ease)
      // ...
    ```

3. Nested selectors

    Nested selectors, _if necessary_, go last, and nothing goes after them. Add whitespace between your rule declarations and nested selectors, as well as between adjacent nested selectors. Apply the same guidelines as above to your nested selectors.

    ```scss
    .btn
      background: green
      font-weight: bold
      transition(background 0.5s ease)

      .icon
        margin-right: 10px

    ```

### Variables

Prefer camelCased variable names (e.g. `myVariable`) over dash-cased or snake_cased variable names. It is acceptable to prefix variable names that are intended to be used only within the same file with an underscore (e.g. `_myVariable`).

All variables are assigned using the `=` symbol with one space before and after the `=` symbol.

Color variables should follow the naming convention of prepending the name of the color with the word **color**, this assists with auto suggest as typing color will suggest all color variables.

Font variables follow the same convention as the color variables where the word **font** precedes the font name.

**Bad**

```scss
my-color = #efefef;
homePurple = #r99812;
roboto = 'Roboto', sans-serif
nunito-font = 'Nunito', sans-serif
```

**Good**

```scss
//Colours
colorGrey = #efefef
colorHomePurple = #r99812

//Fonts
fontRoboto = 'Roboto', sans-serif
fontNunito = 'Nunito', sans-serif


```

[Stylus Variable Documentation](http://stylus-lang.com/docs/variables.html)

### Mixins

Mixins should be used to DRY up your code, add clarity, or abstract complexity--in much the same way as well-named functions. Mixins that accept no arguments can be useful for this.

### Code Example

```html
<div class="btn btn-primary">
  <icon class="icon email-icon"></icon>
  But Now
</div>
```

**Bad**

```scss
.btn
  color: red
  border:2px solid white

.btn.btn-primary
  background: blue

.btn.btn-primary .icon.email-icon
  color: blue
  border:2px solid black
```

**Good**

```scss
button()
  color: red
  border:2px solid white

.btn
  button()
  &.btn-primary
    background: blue

  &.btn-warning
    color red
    .icon
      &.email-icon
        font-size 12pt

```

**[⬆ back to top](#table-of-contents)**
