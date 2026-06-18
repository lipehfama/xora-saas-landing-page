# Tailwind CSS v4 Notes

This project uses Tailwind CSS v4 with the Vite plugin.

## Vite Plugin

Tailwind is registered in `vite.config.ts`:

```ts
plugins: [vue(), tailwindcss()]
```

The plugin must be inside the `plugins` array. It should not be added as a top-level `tailwindcss()` property.

## CSS Entry

The main stylesheet imports Tailwind and the project styles:

```css
@import "tailwindcss";

@import "./theme.css";
@import "./utilities.css";
```

`main.css` is imported once from `src/main.ts`.

## CSS-First Theme

Tailwind v4 supports CSS-first theme tokens through `@theme`.

This project defines tokens in `src/assets/styles/theme.css`, including:

- colors such as `p1`, `p2`, `s1`, and `s2`
- font families
- shadows
- spacing values
- border radii
- line heights
- z-index values

Example:

```css
@theme {
  --color-p1: #2ef2ff;
  --spacing-1230: 1230px;
  --radius-40: 40px;
}
```

Those tokens become utilities such as:

```txt
text-p1
w-1230
rounded-40
```

## Custom Utilities

Tailwind v4 is stricter about applying unknown classes. Classes like `small-2`, `base-bold`, `g7`, and `before:g7` need to exist as real utilities.

This project defines custom utilities with `@utility` in `utilities.css`:

```css
@utility g7 {
  background: linear-gradient(#1b275a, #0e1434);
}
```

That makes variant usage possible:

```txt
md:g7
max-md:h5
```

## Unknown Utility Errors

Errors like this:

```txt
Cannot apply unknown utility class `small-2`
```

usually mean Tailwind does not know that class at build time.

The fix is to define it with `@utility` or replace it with built-in Tailwind classes.

## Canonical Class Suggestions

Warnings such as:

```txt
leading-[64px] can be written as leading-16
max-w-[1252px] can be written as max-w-313
```

are suggestions from tooling, not build-breaking errors. They point out that the arbitrary value maps to Tailwind's spacing scale. These changes are optional unless the project wants to standardize on scale-based utilities.

## Asset Paths

For files inside `src/assets`, prefer importing assets in Vue components instead of using root-relative paths like `/images/example.svg`.

Use:

```ts
import icon from "@/assets/images/icon.svg";
```

Then:

```vue
<img :src="icon" alt="" />
```

Files in `public` can be referenced from the site root, for example:

```md
![Screenshot](/xora-screen.png)
```
