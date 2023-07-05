---
sidebar_position: 2
---

# Configuration

---
## `rules`
**Description:** Defines a configuration object that is applied globally to every generated class.

**Type:** `object`

---
### `rules.namespace`
**Description:** Applies a namespace to generated classes. For example, `"rules.namespace": "ds-"` will generate classes like:
```css
ds-display:flex
ds-flex-direction:row
/* etc */
``` 
**Type:** `string`

**Default:** `''`

---
### `rules.separator`
**Description:** Overwrites the default separator for generated classes. For example, `"rules.separator": "-"` will generate classes like:
```css
display-flex
flex-direction-row
/* etc */
```
Make sure to escape any special CSS characters, like `:`, `\`, `%`, etc. 

**Type:** `string`

**Default:** `'\\:'`

---
## `stylesheet`
**Description:** Defines a configuration object for the outputted stylesheet.

**Type:** `object`

---
### `stylesheet.buildPath`
**Description:** Defines the directory that the stylesheet will be generated in. If the directory does not exist, it will be created.

**Type:** `string`

**Default:** `'styles/yass/'`

---
### `stylesheet.filename`
**Description:** Defines the filename of the stylesheet. If it exists, it will be overwritten.

**Type:** `string`

**Default:** `'yass.css'`

---
### `stylesheet.include`
**Description:** Defines a configuration object for which groups of atomic classes will be included in the generated stylesheet.

**Type:** `object`

---
#### `stylesheet.include.baseClasses`
**Description:** Whether or not to generate the base CSS styles, like `display:flex`.

**Type:** `boolean`

**Default:** `true`

---
#### `stylesheet.include.tokenClasses`
**Description:** Whether or not to generate the token classes, like `padding:space.100`.

**Type:** `boolean`

**Default:** `true`

---
#### `src`
**Description:** Relative directory that points to your source folder, for example: `"./src"`. If set, Just In Time compilation will be enabled. Read more about JIT Yass [here](/docs/jit)

**Type:** `boolean`

**Default:** `true`
