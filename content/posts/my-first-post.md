+++
date = '2025-11-08T19:48:23-05:00'
draft = false
title = 'My First Post'
+++

## Step-by-Step Debugging Process

### 1. __Check Package Dependencies__

- __Action__: Read `package.json` to verify Tailwind CSS installation and version.
- __Why__: Ensures the correct version (v4.1.17) is installed. In this project, both `tailwindcss` and `@tailwindcss/cli` are at v4.1.17.
- __Debugging Tip__: If missing or wrong version, run `npm install tailwindcss@latest @tailwindcss/cli@latest`.

### 2. __Examine Configuration__

- __Action__: Look for `tailwind.config.js` or check CSS for v4-style configuration.
- __Why__: Tailwind v4 uses CSS-based config with `@import "tailwindcss"` and `@source` directives instead of JS config files.
- __Debugging Tip__: In v4, configuration is in the CSS file itself.

### 3. __Review CSS Integration__

- __Action__: Read the main CSS file (`themes/mytheme/assets/css/main.css`).
- __Why__: Found `@import "tailwindcss";` and `@source "hugo_stats.json";` - this is the v4 syntax for importing Tailwind and specifying content sources.
- __Debugging Tip__: Ensure `@import "tailwindcss"` is present; missing it means no Tailwind styles.

### 4. __Check Hugo Integration__

- __Action__: Examine Hugo layout partials (e.g., `head/css.html`) and `hugo.toml`.
- __Why__: Hugo uses `css.TailwindCSS` pipe to process CSS. `hugo.toml` enables build stats for content detection.
- __Debugging Tip__: Verify `{{ . | css.TailwindCSS }}` in layouts; without it, Tailwind won't process.

### 5. __Inspect Build Scripts__

- __Action__: Check `package.json` scripts and Hugo config.
- __Why__: No custom build scripts needed; Hugo handles Tailwind compilation internally.
- __Debugging Tip__: If using custom PostCSS, ensure it's configured for Tailwind v4.

### 6. __Build the Site__

- __Action__: Run `hugo` to generate the site.
- __Why__: Triggers Tailwind compilation via Hugo's CSS pipe.
- __Debugging Tip__: Use `hugo --gc` to clear cache if styles don't update.

### 7. __Verify Generated CSS__

- __Action__: Read the built CSS file (`public/css/main.css`).
- __Why__: Confirms Tailwind styles are included. Initially only base styles and `.block` were present.
- __Debugging Tip__: Look for `/*! tailwindcss v4.x.x */` comment and utility classes in `@layer utilities`.

### 8. __Test Specific Classes__

- __Action__: Add Tailwind classes to a layout (e.g., `class="bg-red-500 text-white"` in `page.html`), rebuild, and check CSS.
- __Why__: Ensures content detection works. Initially, classes in layouts weren't detected because only `hugo_stats.json` was sourced.
- __Debugging Tip__: Add `@source "../layouts/**/*.html"` to CSS to include layout files in content scanning.

## Key Findings

- Tailwind CSS v4 __is working__ in this project.
- The issue was that layout files weren't being scanned for classes by default.
- Adding `@source "../layouts/**/*.html"` to the CSS file fixed the content detection.
- After the fix, `bg-red-500` and `text-white` utilities were properly generated in the CSS.

## Additional Debugging Tips

- Use `hugo server` for development to see live changes.
- Check browser dev tools to inspect if classes are applied.
- If issues persist, verify Hugo version supports Tailwind v4 (requires Hugo 0.128+).
- For custom config in v4, use `@config` directive in CSS instead of JS files.

This process teaches systematic debugging: start with dependencies, check configuration, verify integration, test compilation, and validate output.
