# template-screen-html

Starter template for plain HTML screen apps on the Phystack digital signage platform. Used by `@phystack/cli` to scaffold new projects -- not deployed directly.

## Overview

This template provides a minimal HTML screen app with built-in placeholder replacement for text and image settings. Developers use the Phystack CLI to scaffold a new project from this template, then customize the HTML, styles, and settings schema to build their screen app.

The included `apply-settings.js` runtime listens for the `GridappReady` event from `screen-boot`, reads settings via `window.gridapp.getSettings()`, and replaces mustache-style placeholders (`{{txt:key:description}}`, `{{img:key:description}}`) throughout the DOM before firing `DOMContentLoaded`.

## Tech Stack

| Layer | Technology |
|-------|------------|
| Runtime | Browser (loaded by screen-boot) |
| Language | HTML, CSS, vanilla JavaScript |
| Animations | animate.css |
| Dev server | http-server |
| Build | rsync + `phy app build` |

## Prerequisites

- Node.js 16+
- Yarn or npm

## Getting Started

After scaffolding a new project from this template:

```bash
yarn install
yarn start        # opens http-server on localhost:8080
```

To build and publish to the Phystack app registry:

```bash
yarn build        # copies files to build/ and runs phy app build
yarn pub          # publishes to the registry
```

## Project Structure

```
index.html              # Main screen app markup with placeholders
apply-settings.js       # Runtime: replaces placeholders with settings values
schema.json             # JSON Schema for console-editable settings
default.settings.json   # Default settings used during local development
animate.min.css         # CSS animation library
DESCRIPTION.md          # App listing description (published to registry)
meta/                   # Screenshots for the app registry listing
manifest.json           # PWA manifest
```

## Usage

The Phystack CLI scaffolds a new HTML screen app from this template:

```bash
phy app create --template html
```

This copies all files into a new directory, prompts for an app name, and updates `package.json` accordingly. Developers then edit `index.html`, `schema.json`, and styles to build their screen app.

## Template Variables

Settings are defined in `schema.json` and injected at runtime (not at scaffold time). The placeholder syntax used in HTML files:

| Syntax | Type | Example |
|--------|------|---------|
| `{{txt:key:description}}` | Text replacement in DOM text nodes | `{{txt:productName:The product name}}` |
| `{{img:key:description}}` | Image URL replacement in `src` attributes | `{{img:logo:Company logo}}` |

The `apply-settings.js` script also replaces placeholders found in `style` and `source` attributes.

Default schema properties included in this template:

| Property | Type | Description |
|----------|------|-------------|
| `productName` | string | Display name shown on screen |
| `productPrice` | string | Price label shown on screen |

## Settings Schema

The `schema.json` file defines which fields appear in the Phystack console for content editors. It follows standard JSON Schema. The corresponding `default.settings.json` provides fallback values for local development.

## Related Documentation

- [Phystack CLI](https://github.com/phystack/cli) -- scaffolding and publishing commands
- [screen-boot](https://github.com/phystack/screen-boot) -- runtime that loads screen apps on devices
