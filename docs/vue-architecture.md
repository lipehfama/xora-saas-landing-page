# Vue 3 Architecture

This project uses Vue 3 single-file components with the Composition API and `<script setup>`. The page is composed from section components instead of routing between pages, because the product is a single landing page.

## Main Composition

`src/App.vue` is responsible for arranging the page sections:

```txt
Header
Hero
Features
Pricing
Faq
Testimonial
Download
Footer
```

This keeps the top-level structure easy to scan and lets each section own its own layout.

## Component Categories

- `components/layout`: persistent layout components such as the header and footer.
- `components/sections`: full-page landing sections.
- `components`: reusable UI pieces used by multiple sections.
- `constants`: structured data used to render repeated UI.
- `assets/styles`: Tailwind entry file, design tokens, and custom utilities.

## Content Constants

Repeated content lives in `src/constants/index.ts`. This keeps templates focused on rendering and reduces duplicated markup.

Examples include:

- feature cards
- pricing plans
- FAQ items
- testimonials
- platform links
- partner logos

The arrays use `as const` so TypeScript preserves literal values and gives better inference when those constants are passed into components.

## Props

Reusable components receive explicit TypeScript props. For example, `PricingCard.vue` receives a single `plan`, plus state telling it whether the plan is primary and whether monthly pricing is active.

This keeps the pricing logic in one place:

- `Pricing.vue` owns the monthly/yearly toggle.
- `PricingCard.vue` renders the calculated card state.

## Asset Imports

In Vue and Vite, assets inside `src/assets` should usually be imported from scripts:

```ts
import logo from "@/assets/images/xora.svg";
```

Then the template can bind them:

```vue
<img :src="logo" alt="Xora logo" />
```

This avoids broken paths when files are bundled for production.

## Header Behavior

The header tracks scroll position and the active section. The navigation links are real `<a>` elements, but their click behavior uses smooth scrolling and updates active state.

The important ideas are:

- use anchor semantics for navigation
- update active state based on visible section
- close the mobile menu after navigation
- keep scroll work lightweight

## Semantic HTML

The project uses semantic structure where it helps accessibility:

- `<header>` for the main navigation
- `<main>` for the page content
- `<section>` for major page sections
- `<article>` for independent cards and testimonials
- `<nav>` for navigation groups
- `<ul>` and `<li>` for repeated lists
- `<blockquote>` and `<cite>` for testimonials

Good semantics make the page easier for screen readers, crawlers, and future maintainers to understand.
