# Transformers

Transformers are the core of Yass. They are responsible for turning a design token, like:

```json
{
  "key": "space.100",
  "value": "8px",
  "properties": ["padding"] 
}
```
into a Yass stylesheet like:
```css
:root{
  --space.100: 8px;
}

.padding\\:space.100 {
  padding: var(--space.100);
}
```

Under the hood they use `postCSS` to generate declarations for rules, and append them to an AST. Yass currently has the following transformers:

## `BaseCSSTransformer`
`BaseCSSTransformer` is responsible for generating Yass atomic CSS classes that don't rely on design tokens. For example: `display:flex`.

`BaseCSSTransformer` is under active development and likely to change in future. Currently it generates atomic CSS classes from an internally defined list of CSS properties. This is not ideal, since as the CSS spec changes, the internal list needs to be updated, meaning older versions of Yass will generate out of date stylesheets. Ideally, this list would be maintained independently, meaning any version of Yass can generate an up-to-date stylesheet. This section will be more fully documented when this is achieved.


## `AtomicClassTransformer`
`AtomicClassTransformer` is responsible for generating atomic classes. It takes a `DesignToken[]`:

```json
[
  {
    "key": "blue-500",
    "value": "#0063bd",
    "properties": ["color"]
  },
]
```
and outputs an `AtomicClass[]`. `AtomicClass` is a wrapper around a `postCSS` class declaration that has been tailored to suit Yass classes. `AtomicClass` will enforce a single rule per class, auto format the class to be on one line, and adds functionality like `toString()` and `toJSON()`:
```typescript
const config: Config = getConfig({})
const tokens: DesignToken[] = [
  {
    key: 'blue-500',
    value: '#0063bd',
    properties: ['color']
  },
]

const result = AtomicClassTransformer.transform(tokens, config)
  .map((atomicClass: AtomicClass) => 
    atomicClass.toString())

// `result` will be: [".color\\:blue-500 { color: var(--blue-500); }"]
```

Note that the value is set to a CSS custom property (`var(--blue-500)`), however, `--blue-500` is not defined in the output of `AtomicClassTransformer.transform()`. This responsibility is delegated to: `CustomPropertyTransformer`. `AtomicClassTransformer` uses `CustomPropertyTransformer` internally to ensure that the custom properties that are set inside the atomic classes match the custom property declarations inside `:root`.

## `CustomPropertyTransformer`

`CustomPropertyTransformer` is responsible for generating CSS custom property definitions that are set in the `:root` element. For example:
```typescript
const config: Config = getConfig(userConfig)
const tokens: DesignToken[] = [
  {
    key: 'blue-500',
    value: '#0063bd'
  },
]

const result = CustomPropertyTransformer
  .transform(tokens, config)
  .map((customProperty: CustomProperty) => 
    customProperty.toString())

// `result` will be: ["--blue-500: #0063bd"]
```

## `ThemeTransformer`
