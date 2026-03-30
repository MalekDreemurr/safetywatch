# AGENTS.md — SafetyWatch Dark Theme Project

## Project Overview

SafetyWatch is a workplace safety monitoring application with AI-driven violence detection and automated attendance tracking. This repository contains the dark theme variant of the application.

## Project Structure

```
safety-watch-dark/
├── safetywatch.html           # Main landing page
├── css/
│   └── style-dark.css         # Main stylesheet (dark/light theme support)
└── pages/
    ├── safetywatch-login.html
    ├── safetywatch-signup.html
    ├── safetywatch-dashboard.html
    ├── safetywatch-my-dashboard.html
    ├── attendance-logs.html
    ├── attendance-logs-admin.html
    ├── camera-management.html
    ├── employees.html
    ├── security-alerts.html
    └── violation-logs.html
```

## Build/Lint/Test Commands

This is a **static HTML/CSS project** with no build system, test framework, or linter configured.

- **Preview**: Open `safetywatch.html` directly in a browser, or serve via any static server:
  ```bash
  # Python
  python -m http.server 8000
  # Node.js (npx)
  npx serve .
  ```
- **Single-page testing**: Each HTML file is self-contained and can be tested individually
- **No CI/CD pipeline** currently configured

## Code Style Guidelines

### General Principles

- Use semantic HTML5 elements (`<nav>`, `<main>`, `<section>`, `<article>`, `<footer>`)
- Ensure accessibility: include `alt` attributes, ARIA labels where needed, keyboard-navigable interactive elements
- Keep functionality simple — this is a static site, not a SPA

### HTML Conventions

- Use **2-space indentation** for HTML nesting
- All HTML files must have proper doctype and lang attribute:
  ```html
  <!DOCTYPE html>
  <html lang="en">
  ```
- Self-close void elements (e.g., `<br />`) only when serving XML/XHTML
- Use double quotes for attributes: `<a href="page.html">`
- Group related elements logically and use comment headers for sections:
  ```html
  <!-- NAV -->
  <nav>...</nav>

  <!-- MAIN CONTENT -->
  <main>...</main>
  ```

### CSS Conventions

- **2-space indentation** for CSS rules
- Use **CSS custom properties (variables)** for all color and design tokens
- Follow the established token naming pattern: `--bg`, `--surface`, `--border`, `--text-primary`, `--text-secondary`, `--accent`, `--green`, `--red`, `--orange`, `--gray`
- Box-sizing reset at the top of stylesheets:
  ```css
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
  ```
- Use shorthand properties where appropriate (`margin: 0` vs `margin-top: 0; margin-right: 0; ...`)
- Use `rem` for sizing, `em` for font-relative spacing
- Use `rgba()` for transparent shadows and overlays
- Comment section headers with box-drawing characters:
  ```css
  /* ═══════════════════════════════════════════════════════════════
     SECTION NAME
     ═══════════════════════════════════════════════════════════════ */
  ```

### Theme System

The project uses a CSS custom property-based theming system:

- **Dark mode** is the default (no `data-theme` attribute or `data-theme="dark"`)
- **Light mode** is triggered via `data-theme="light"` on the `<html>` element
- JavaScript toggles theme by setting `localStorage.getItem('theme')` and updating the attribute:
  ```javascript
  document.documentElement.setAttribute('data-theme', t);
  ```
- All color overrides for light mode must be inside `[data-theme="light"]` selector

### Naming Conventions

- **CSS classes**: kebab-case (e.g., `nav-btns`, `theme-toggle`, `icon-sun`)
- **CSS custom properties**: kebab-case with descriptive names (e.g., `--accent-soft`, `--gray-400`)
- **HTML ids**: kebab-case (e.g., `id="home"`, `id="architecture"`)

### Color Palette (Design Tokens)

| Token | Dark Mode | Light Mode | Purpose |
|-------|-----------|------------|---------|
| `--bg` | `#0f1419` | `#f0f2f5` | Page background |
| `--surface` | `#1a2029` | `#ffffff` | Cards, panels |
| `--border` | `#2a323d` | `#e4e8ef` | Borders, dividers |
| `--text-primary` | `#e2e8f0` | `#0d1b3e` | Main text |
| `--text-secondary` | `#94a3b8` | `#7a8599` | Muted text |
| `--accent` | `#3b82f6` | `#1a3cff` | Primary actions |
| `--green` | `#10b981` | `#10b981` | Success states |
| `--red` | `#ef4444` | `#ef4444` | Error/danger states |
| `--orange` | `#f59e0b` | `#f59e0b` | Warning states |

### Accessibility Requirements

- All interactive elements must have visible focus states
- Use `aria-label` on icon-only buttons
- Ensure color contrast meets WCAG AA standards (4.5:1 for normal text, 3:1 for large text)
- Provide `title` attributes on SVGs used as icons
- Use `<button>` for actions, `<a>` for navigation

### Error Handling

- Form validation should use HTML5 validation attributes (`required`, `pattern`, `type`)
- For any JavaScript error scenarios, log to console with descriptive messages
- Gracefully degrade if localStorage is unavailable (wrap in try/catch)

### Working with This Codebase

1. **Do not add JavaScript files** — all JS is inline within `<script>` tags in HTML
2. **Do not add build tools** — this project intentionally remains static
3. **Test changes in browser** — use a local server to avoid CORS issues with localStorage
4. **Preserve the theme toggle** — any UI changes should maintain the dark/light theme switcher functionality
5. **Keep SVGs inline** — icons are embedded as inline SVG for styling flexibility

### File Size Considerations

- The main `style-dark.css` is ~2000 lines; avoid adding more styles unless necessary
- Optimize any new SVGs before adding them
- Prefer CSS solutions over adding images
