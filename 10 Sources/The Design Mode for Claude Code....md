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


```
Help me rebuild the exact same header-mobile component UI design as the html provided,here is the extracted css, and an image of the UI is also provided
Use tailwind and associated styling within a single code block. Default to using tailwind however, if CSS styles must be placed directly within the `style` attribute.
Unless a specific style is provided, design should align with a modern, clean aesthetic (e.g., similar to Linear, Stripe, Vercel, or Tailwind UI's design principles
If design specifications, code, or HTML are provided, **(IMPORTANT: respect the original design, fonts, colors, and style as much as possible)

```
Use [VisBug](https://chromewebstore.google.com/detail/visbug/cdockenadnadldjbbgcallicgledbeoc?pli=1) to fix the differences and gaps and fix them

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

**Create UI based on the style*
```
Help me design a personal todo UIbased on the style in todo.html
```

use the ui-design guidelines prompt with the above
```
*   **Code Structure:** Update the provided HTML tailwind and associated styling within a single code block. Default to using tailwind however, if CSS styles must be placed directly within the `style` attribute.
*   **Response Format:** Begin with a textual response, then provide the code, and conclude with a final response.
*   **Prohibited Mentions:** Do not mention tokens, Tailwind, or HTML in your response.
*   **Iconography:** Use Lucide icons with a 1.5 stroke width.
*   **Aesthetic Style:** Unless a specific style is provided, design should align with a modern, clean aesthetic (e.g., similar to Linear, Stripe, Vercel, or Tailwind UI's design principles). **(IMPORTANT: Do not mention these specific brand names).**
*   **Custom UI Elements:** If checkboxes, sliders, dropdowns, or toggles are required, they should be custom-designed within the provided code (do not add them unless they are part of the requested UI).
*   **Typography Accuracy:** Be extremely accurate with font choices.
*   **Font Weight Adjustment:** For font weights, use one level thinner than the common naming; for example, "Bold" should be rendered as "Semibold."
*   **Title Tracking:** Titles with a font size above 20px should use `tracking-tight`.
*   **Responsiveness:** Ensure the design is responsive.
*   **Styling Application:** Avoid setting Tailwind configuration or defining CSS classes; apply utility classes directly to HTML tags.
*   **Chart Implementation:** If charts are included, use Chart.js. (To prevent potential layout issues, if a canvas element is at the same level as other block nodes, embed it within a `<div>` to ensure proper sizing, e.g., `<h2><p><div><canvas></canvas></div></p></h2>` rather than `<h2><p><canvas></canvas></p></h2>`).
*   **Visual Separation:** Add subtle dividers and outlines where appropriate.
*   **Root Class Application:** Do not apply utility classes to the `<html>` tag; apply them to the `<body>` tag.
*   **Image Sourcing:** If no images are specified, use Unsplash images (e.g., faces, 3D renders).
*   **Design Creativity:** Be creative with fonts and layouts, be extremely detailed, and prioritize functionality.
*   **Respect Original Design:** If design specifications, code, or HTML are provided, **(IMPORTANT: respect the original design, fonts, colors, and style as much as possible).**
*   **Animation Method:** Do not use JavaScript for animations; use CSS transitions and transformations instead.
*   **Interactive Feedback:** Include hover color and outline interactions.
*   **Theming - Dark Mode:** For "tech," "cool," or "futuristic" themes, favor dark mode, unless otherwise specified.
*   **Theming - Light Mode:** For "modern," "traditional," "professional," or "business" themes, favor light mode, unless otherwise specified.
*   **Icon Styling:** Use a 1.5 stroke width for Lucide icons and avoid gradient containers for icons.
*   **Visual Contrast:** Employ subtle contrast.
*   **Logo Design:** For logos, use letters only with tight tracking.
*   **Prohibited Button:** Avoid placing a bottom-right floating "DOWNLOAD" button.
```