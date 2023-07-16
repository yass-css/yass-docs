# Pseudo Selectors

All Yass atomic classes can be modified to trigger for pseudo selectors.

## Pseudo Classes
To apply a pseudo class to a Yass class, simply append it to the end of the class name. For example:
```html
<button class="
  background-color:blue-500
  background-color:blue-400:hover
  background-color:blue-600:active
">
  Click Me!
</button>
```

Assuming you have supplied `blue-400`, `blue-500`, `blue-600` tokens, the above example will style the `button` with a `blue-500` background initially. When the use hovers on the button, `blue-400` will be applied, and when the use clicks the button `blue-600` will be applied.

When in JIT mode, Yass currently supports all pseudo-classes defined [here](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes). 
When not in JIT mode, Yass will generate most pseudo-classes. However, there are some it is unable to generate because the permutation space is infinitely large. For example, take `border-style:solid:nth-child(2n+1)`. There is no way for Yass to generate every possible argument passed to `nth-child`, so it is impossible to generate such pseudos unless the JIT compiler searches through your source code. The full list of pseudo-classes that are only generated in JIT mode is:
  - `:dir()`
  - `:has()`
  - `:host()`
  - `:host-context()`
  - `:is()`
  - `:lang()`
  - `:not()`
  - `:nth-child()`
  - `:nth-col()`
  - `:nth-last-child()`
  - `:nth-last-col()`
  - `:nth-last-of-type()`
  - `:nth-of-type()`
  - `:state()`
  - `:where()`

### Chaining
When in JIT mode, Yass can generate arbitrary permutations of chained pseudo-selectors. For example, `border-style:solid:hover:focus` will generate the following class definition:

```css
.border-style\:solid\:hover\:focus:hover:focus { 
  border-style: solid;
}
```

There are a few things about this that might be confusing, so let's break it down into pieces.

Firstly, the `border-style:solid:hover:focus` selector requires the class name to match, including the order of the pseudos. So, the first part of the class definition (`.border-style\:solid\:hover\:focus`) is the same as the selector, except with the special characters like `':'` escaped, and transformed into a class name, by prepending `.`.

The second part of the class name is the actual pseudo. If you ignore the complicated first chunk, it's just like a regular CSS class:
```css
.my-button:hover:focus {
  border-style: solid;
}
```

So, after the section of the class name that matches the selector, the pseudos are simply appended in the same order the user defined.

Note: The implementation of chained pseudos deliberately matches the CSS spec, where a class with `:hover:focus` will be applied only when `:hover` *and* `:focus` are true, not `:hover` *or* `:focus`.

### More complex pseudos

While in JIT mode, Yass is capable of generating much more complex pseudo-classes, such as pseudo-classes that take arguments, like: `:nth-child(2n + 1)`. This is because JIT compilation allows Yass to inspect your source code for patterns that match selectors, such as: `<some-css-property>:<some-design-token>:nth-child(<arbitrary-argument>)`. This means you are able to write code like:
```html
<ul class="
    background-color:neutral-100
    background-color:neutral-200:hover
  "
>
  <li>First</li>
  <li>Second</li>
  <li>Third</li>
</ul>
```


## Pseudo Elements
Pseudo elements are currently not supported in Yass.

## Disabling
When not using JIT mode, pseudo-selectors can be disabled via the `yass.config.json` via the [`stylesheet.include.pseudos`](/yass-docs/docs/configuration#stylesheetincludepseudos) configuration setting.
