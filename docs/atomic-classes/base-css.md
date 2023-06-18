---
sidebar_position: 3
---

# Base CSS Classes

By default, Yass will generate atomic CSS classes for every appropriate CSS property. For example:

```css
.display:flex {
  display: flex;
}
```

## Disabling

If you wish to disable base CSS class generation, you can do so by in your `yass.config.json`:
```json
{
  "stylesheet": {
    "include": {
      "baseClasses": false,
    }
  }
}
```

See <a href="/docs/configuration#stylesheetincludebaseclasses">baseClasses</a> for more information.
