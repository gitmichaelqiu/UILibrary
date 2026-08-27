# Zensical Documentation Site

A reusable Zensical configuration and theme foundation extracted from the
shared settings used by the `mqiu.dev/blog` and
`docs.desktoprenamer.mqiu.dev` websites.

## Includes

- A placeholder `zensical.toml` with responsive navigation, palette switching,
  Material features, and common Markdown extensions.
- `brand-theme.css` for Klein blue, pale silver, Inter typography, restrained
  borders, content cards, navigation, and the large footer banner.
- `theme-override.css` for stable light/dark colors and palette-toggle scroll
  behavior.
- Shared sheet-table and pan/zoom component styles.
- An `overrides/main.html` hook that preserves scroll position while changing
  color palettes and renders the branded footer banner.

## Usage

Copy this folder into a Zensical project, replace the placeholder project
metadata and navigation in `zensical.toml`, and add the referenced logo and
favicon under `docs/images/`. Keep project-specific Markdown, assets, and
JavaScript in the consuming site.

The `pan_zoom.css` and `sheet.css` files are optional component styles. Remove
them from `extra_css` when the site does not use those components.

## Source

This is a reusable snapshot of the shared configuration and styling patterns in
the mqiu.dev Zensical sites. It intentionally omits their content, branding
assets, generated sites, caches, virtual environments, and custom sync tools.
