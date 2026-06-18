# Performance and SEO Notes

This project was checked with Lighthouse during development. The main findings were related to image delivery, development-server overhead, and basic metadata.

## Lighthouse and Development Mode

Running Lighthouse against `pnpm dev` can produce misleading JavaScript warnings because the Vite development server serves unbundled modules and the Vite client.

For more realistic performance results, use:

```bash
pnpm build
pnpm preview
```

Then audit the preview URL in an incognito browser profile without extensions.

## Image Delivery

Large images can dominate LCP. The hero image was the largest candidate because it is visible above the fold.

Useful techniques:

- use modern formats such as WebP or AVIF
- provide responsive image sizes with `srcset`
- set explicit `width` and `height`
- use `fetchpriority="high"` for the LCP image
- lazy-load images below the fold

Example:

```vue
<img
  :src="fallbackImage"
  :srcset="`${mobileImage} 560w, ${tabletImage} 820w, ${desktopImage} 1230w`"
  sizes="(max-width: 767px) 560px, (max-width: 1023px) 820px, 1230px"
  width="1230"
  height="1230"
  fetchpriority="high"
  loading="eager"
  decoding="async"
  alt="Xora AI video editor interface preview"
/>
```

## Lazy Loading

Images that appear below the first viewport should usually use:

```html
loading="lazy"
decoding="async"
```

The hero image should not be lazy-loaded because it is the LCP element.

## Fonts

External fonts can be render-blocking. This project uses Google Fonts, so the request should include only the weights actually needed by the design.

Good practices:

- keep `preconnect` for Google font origins
- avoid requesting every weight
- include `display=swap`
- consider self-hosting fonts for stricter performance goals

## SEO Basics

The project includes:

- a descriptive `<title>`
- a meta description
- favicon links
- a valid `robots.txt`
- semantic page sections
- descriptive image alternatives where images are informative

## Accessibility Notes

Lighthouse also flagged structural issues during development. Fixes included:

- ensuring `<ul>` elements contain only `<li>` children
- using empty `alt=""` for decorative images
- avoiding duplicate image alt text where adjacent text already explains the item
- using real anchor tags for navigation
- adding labels for icon-only links and buttons
