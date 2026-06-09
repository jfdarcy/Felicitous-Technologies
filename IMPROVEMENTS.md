# Potential Improvements

A pre-production review of the Felicitous Technologies site (`index.html`, `css/styles.css`, `js/main.js`). Item #10 (automate copyright year) has been completed and is omitted.

## High priority

### 1. Missing favicon and social/SEO meta tags
A good `description` exists, but production needs:
- A favicon (`<link rel="icon">`) — browsers request `/favicon.ico` by default and it'll 404 otherwise.
- Open Graph / Twitter Card tags (`og:title`, `og:description`, `og:image`, `og:url`) so shared links render nicely on LinkedIn/Slack/Twitter.
- A canonical URL (`<link rel="canonical">`).
- `<meta name="theme-color">` for mobile browser chrome.

### 2. Nav references a section ID that doesn't exist consistently
The nav menu links to `#home`, `#services`, `#products`, `#contact`, but there's an `#about` section with no nav link. The active-nav-highlight JS tracks all `section[id]`, so when scrolling into About, no link highlights. Either add an About link or be intentional about it.

### 3. Real logo / social share image
The logo is text-only. Consider a real logo asset and a social share image (`og:image`) for a production tech company site.

## Medium priority

### 4. `loading` class is removed but never added
`js/main.js` removes a `loading` class from body, but it's never added in HTML or CSS. Dead code — suggests an intended FOUC-prevention pattern that was never finished. Either remove it or implement the loading state.

### 5. Scroll reveal can hide content if JS fails
The `.reveal` class sets `opacity: 0` and is only added via JS, so no-JS users are safe. The hero isn't in the reveal list, so things are okay — but consider a `<noscript>` fallback or ensuring above-the-fold content never depends on the observer.

### 6. `transitionDelay` on reveal can feel sluggish
`el.style.transitionDelay = \`${index * 0.1}s\`` indexes across all reveal elements globally (cards, features, stats, headers), so later elements can have a 1s+ delay and feel slow to appear. Reset the index per-section or cap the delay.

### 7. Duplicate `.hero__actions` rule
The 768px and 480px media queries both set the same `flex-direction: column; width: 100%` on `.hero__actions`. The 480px one is redundant since 768px already covers it.

### 8. `lastScroll` is tracked but unused
`js/main.js` maintains `lastScroll` but never reads it. Leftover from a likely hide-on-scroll-down header feature. Safe to remove.

## Low priority / polish

### 9. Email-only contact
The only contact path is a `mailto:` link. Fine for a small site, but a real form (with spam protection) tends to convert better. Optional.

### 11. Reduced-motion support
Several transforms, transitions, and scroll-reveal animations exist. Add a `@media (prefers-reduced-motion: reduce)` block to disable animations for users who request it.

### 12. `scroll-behavior: smooth` + JS smooth scroll overlap
CSS sets `scroll-behavior: smooth` and JS also does manual `window.scrollTo({ behavior: 'smooth' })`. Not a bad conflict, but the JS is redundant given CSS already handles it (and `scroll-padding-top: 5rem` handles the header offset). Could simplify by relying on CSS alone.

## Already solid (no action needed)
- Semantic HTML (`<header>`, `<main>`, `<section>`, `<article>`, `<footer>`).
- External links use `rel="noopener noreferrer"` correctly.
- `passive: true` on scroll listeners — good for performance.
- Responsive, fluid typography via `clamp()`.
- IIFE with `'use strict'` — no global pollution.
