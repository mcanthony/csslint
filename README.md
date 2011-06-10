# CSSLint

## Introduction

CSSLint is a tool to help point out problems with your CSS code. It does basic syntax checking as well as applying a set of rules to the code that look for problematic patterns or signs of inefficiency. The rules are all pluggable, so you can easily write your own or omit ones you don't want.

## The CSSLint Rules

### Parsing errors should be fixed

By default, CSSLint shows any parsing errors. Parsing errors usually mean you mistyped a character and may cause the browser to drop your rule or a property. Parsing errors are presented as errors by CSSLint, the most important issues to fix.

### Don't use adjoining classes

Adjoining classes look like `.foo.bar`. While technically allowed in CSS, these aren't handled properly by Internet Explorer 7 and earlier.

### Remove empty rules

Any rule that doesn't contain any properties, such as:

```css
.foo {
}
```
    
A lot of times, empty rules appear as a result of refactoring without further cleanup. Eliminating empty rules results in smaller file sizes and less style information for the browser to deal with.

### Use correct properties for a display

Even though you can define any group of properties together in a CSS rule, some of them will be ignored due to the `display` of the element. This leads to extra cruft in the CSS file. The list of properties that CSSLint checks for are:

* `display: inline` should not use `width`, `height`, `margin` (and all variants), `padding` (and all variants), or `float`.
* `display: inline-block` should not use `float`.
* `display: block` should not use `vertical-align`.
* `display: table-*` should not use `margin` (and all variants) or `float`.

Removed the ignored or problematic properties decreases file size and improves performance.

### Don't use too many floats

Using `float` for layout isn't a great idea, but sometimes you have to. CSSLint simply checks to see if you've used `float` more than 10 times, and if so, displays a warning. Using this many floats usually means you need some sort of abstraction to achieve the layout.

### Don't use too many web fonts

Web fonts are growing in popularity and use of `@font-face` is on the rise. However, using web fonts comes with performance implications as font files can be quite large and some browsers block rendering while downloading them. For this reason, CSSLint will warn you when there are more than five web fonts in a style sheet.

### Don't use too may font-size declarations

A site is typically made up of a finite number of font treatments, including font size. If you have 10 or more font sizes specified, you probably want to refactor into a standard set of font size classes that can be used in markup.

### Don't use IDs in selectors

IDs shouldn't be used in selectors because these rules are too tightly coupled with the HTML and have no possibility of reuse. It's much preferred to use classes in selectors and then apply a class to an element in the page.

### Don't qualify headings

Heading elements (`h1`-`h6`) should be defined as top-level styles and not scoped to particular areas of the page. For example, this is an example of an overqualified heading:

```css
.foo h1 {
    font-size: 110%;
}
```

Heading elements should have a consistent appearance across a site.

### Heading styles should only be defined once

Heading elements (`h1`-`h6`) should have exactly one rule on a site. CSSLint warns if it finds more than one.

### Be careful using width: 100%

Using `width: 100%` on an element whose parent element has padding will result in the child stretching outside of the parent's bounding box. It's generally not a good idea to use `width: 100%`. Instead, use `width: auto` or `display: block`.