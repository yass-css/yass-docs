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

### Supported Pseudo Classes
The following pseudo classes are currently supported:
- `:active`
- `:autofill`
- `:checked`
- `:default`
- `:defined`
- `:disabled`
- `:enabled`
- `:first-child`
- `:first-of-type`
- `:first`
- `:focus-visible`
- `:focus-within`
- `:focus`
- `:fullscreen`
- `:hover`
- `:indeterminate`
- `:invalid`
- `:last-child`
- `:last-of-type`
- `:link`
- `:only-of-type`
- `:optional`
- `:required`
- `:valid`
- `:visited`

### Unsupported Pseudo Classes
The following pseudo classes are currently unsupported, but will likely be supported soon:
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

The following pseudo classes are currently unsupported, and unlikely to be supported ever:
- `:any-link`
- `:blank`
- `:current`
- `:empty`
- `:future`
- `:host`
- `:in-range`
- `:left`
- `:local-link`
- `:modal`
- `:only-child`
- `:out-of-range`
- `:past`
- `:paused`
- `:picture-in-picture`
- `:placeholder-shown`,
- `:playing`,
- `:read-only`
- `:read-write`
- `:right`
- `:root`
- `:scope`
- `:target-within`
- `:target`
- `:user-invalid`

If you feel you have a need for one of these pseudo classes, create a [github issue](https://github.com/yass-org/yass-css/issues).

## Pseudo Elements
Pseudo elements are currently not supported in Yass.
