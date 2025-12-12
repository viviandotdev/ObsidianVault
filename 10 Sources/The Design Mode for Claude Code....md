tags::
source:: https://www.youtube.com/watch?v=vcJVnyhmLS4
type:: #source/article

The Design Mode for Claude Code..

**Rebuild a example design using HI-FI context**
**Context**
- Download the html file
- Inspect and Copy entire style css
**Prompt**
```
Help me rebuild the exact same UI design in single html as motherduck.html, above is the extracted css
```

**Generate a style guide**
```
Great, now help me generate a detailed style guide.

The style guide must include the following sections:

*   Overview
*   Color Palette
*   Typography (Pay attention to font weight, font size, and how different fonts have been used together in the project)
*   Spacing System
*   Component Styles
*   Shadows & Elevation
*   Animations & Transitions
*   Border Radius
*   Opacity & Transparency
*   Common Utility Class Usage (e.g., related to your chosen framework)
*   Example Component Reference Design Code
*   And so on...

In short, provide a detailed analysis and description of the project's style system, ensuring all important details are included.
```

output a styleGuide.md

**Create UI based on the style**
```
Help me design a personal todo UIbased on the style in todo.html
```