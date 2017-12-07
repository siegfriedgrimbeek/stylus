# Eeleven Stylus / CSS in JS Styleguide

Stylus Naming Conventions and Style Guide();

Inspired by the [Airbnb CSS / Sass Styleguide](Airbnb CSS / Sass Styleguide).

## Table of Contents

1. [Terminology](#terminology)
    - [Rule Declaration](#rule-declaration)
    - [Selectors](#selectors)
    - [Properties](#properties)

2. [Stylus](#stylus)
    - [Formatting](#formatting)
    - [ID Selectors](#id-selectors)
    - [JavaScript hooks](#javascript-hooks)
    - [Ordering](#ordering-of-property-declarations)

## Terminology

### Rule declaration

A “rule declaration” is the name given to a selector (or a group of selectors) with an accompanying group of properties. Here's an example:

```scss
.listing
  font-size: 18px
  line-height: 1.2
```

### Selectors

In a rule declaration, “selectors” are the bits that determine which elements in the DOM tree will be styled by the defined properties. Selectors can match HTML elements, as well as an element's class, ID, or any of its attributes. Here are some examples of selectors:

```scss
.my-element-class
  /* ... */

[aria-hidden]
  /* ... */

```

### Properties

Finally, properties are what give the selected elements of a rule declaration their style. Properties are key-value pairs, and a rule declaration can contain one or more property declarations. Property declarations look like this:

```scss
/* some selector */
  background: #f1f1f1;
  color: #333

```


**[⬆ back to top](#table-of-contents)**


## Stylus

### Formatting

* Use soft tabs (2 spaces) for indentation
* Use dashes over camelCase for class names
* Do not use ID selectors
* When using multiple selectors in a rule declaration, give each selector its own line.
* Use a single `:` character for a rule declaration
* * In properties, put a space after, but not before, the `:` character
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

### Ordering of property declarations

1. Property declarations

    List all standard property declarations **first**, that is anything that isn't an `@include` or a nested selector.

    ```scss
    .btn-green
      background: green
      font-weight: bold
    ```

2. `@include` declarations

    Grouping `@include`s at the end makes it easier to read the entire selector.

    ```scss
    .btn-green
      background: green
      font-weight: bold
      @include transition(background 0.5s ease)
      // ...
    ```

3. Nested selectors

    Nested selectors, _if necessary_, go last, and nothing goes after them. Add whitespace between your rule declarations and nested selectors, as well as between adjacent nested selectors. Apply the same guidelines as above to your nested selectors.

    ```scss
    .btn
      background: green
      font-weight: bold
      @include transition(background 0.5s ease)

      .icon
        margin-right: 10px

    ```


**[⬆ back to top](#table-of-contents)**
