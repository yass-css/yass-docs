---
sidebar_position: 1
---

# Quickstart

The simplest way to jump in and see what Yass CSS can do, is to run:
```bash
npx yass-css
```

This will use Yass' default design system to generate a stylesheet full of atomic CSS classes for you to use. By default, the stylesheet will be generated at `styles/yass/yass.css`

However, Yass really shines when you use your own design tokens. If you already have your tokens ready to go, you can just run:

```bash
npx yass-css /path/to/tokens
```

If you don't have any tokens yet, you can create one to test Yass out:

```bash
mkdir my-tokens
touch my-tokens/scale.json
echo '[ { "key": "scale-100", "value": "8px", "category": "scale" } ]' > my-tokens/scale.json
npx yass-css my-tokens
```

If you take a look at the generated stylesheet at `styles/yass/yass.css`, you will see something like this:

```css
/* Your token has been turned into a CSS custom property */
:root {
  --scale-100: 8px;
}

/* And a bunch of relevant styles have been generated that reference the custom property, such as: */
.padding\:scale-100 { padding: var(--scale-100); }
.width\:scale-100 { width: var(--scale-100); }
.gap\:scale-100 { gap: var(--scale-100); }
/* and so on */
```

You can now use these Yass classes to style your site. Create an `index.html` with the following content:

```html
<div class="display:flex flex-direction-column gap:scale-100">
  <h1>Hello from Yass</h1>
  <button>Click me!</button>
</div>
```
