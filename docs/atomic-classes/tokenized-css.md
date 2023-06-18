---
sidebar_position: 3
---

# Tokenized CSS Classes

By default, Yass will generate tokenised atomic CSS classes for every appropriate CSS property. For example, for the following Yass token declaration:
```json
[
  {
    "key": "scale-100",
    "value": "8px",
    "properties": ["padding"],
  }
]
```

Yass will generate the following CSS custom property, and atomic class:
```css
:root {
  --scale-100: 8px;
}

.padding:scale-100 {
  background-color: var(--scale-100);
}
```

## Disabling

If you wish to disable tokenised CSS class generation, you can disable it in your `yass.config.json`:
```json
{
  "stylesheet": {
    "include": {
      "tokenClasses": false,
    }
  }
}
```

See <a href="/docs/configuration#stylesheetincludetokenclasses">tokenClasses</a> for more information.
