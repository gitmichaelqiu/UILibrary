# Editorial Portfolio Website

A reusable CSS foundation extracted from the shared styling system used by the
`mqiu.dev` portfolio and product websites.

## Includes

- Light and dark theme tokens under `:root` and `html.dark`.
- Inter, Syncopate, and Playfair Display typography utilities.
- Responsive containers, 12-column content grids, and section layouts.
- Glass surfaces, editorial gradient text, buttons, navigation, cards, and footer styles.
- Cursor-following image/flag presentation styles for JavaScript-enhanced cards.
- Preloader, parallax, mask-reveal, and text-slide animation hooks.

## Usage

Include `main.css` after the project’s utility framework, if one is used. The
stylesheet is intentionally framework-agnostic, but its utility-class examples
assume Tailwind CSS or equivalent utilities for layout composition.

The visual behavior is CSS-only. Add project-specific HTML and JavaScript for
the corresponding class hooks, and replace the default brand tokens before
shipping a site.

## Source

This template is maintained as a reusable snapshot of the shared `mqiu.dev`
website styling. Keep application copy, assets, and page-specific behavior in
the consuming website rather than adding them here.
