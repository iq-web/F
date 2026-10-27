# Anwar Al-Sumoud storefront

## Five-file package

- `index.html` contains the Arabic/RTL document shell, SEO and social metadata,
  Organization JSON-LD, the editable `window.App.CONFIG` data block, critical
  first-paint styles, and the script loading order.
- `styles.css` contains the storefront's complete responsive styles, light/dark
  themes, focus states, transitions, animations, and reduced-motion rules.
- `app.js` is the self-contained production application bundle. It implements
  routing, catalog/search/filtering, product details, request lists, quote
  forms, WhatsApp handoff, localization, theme selection, storage, and
  accessibility behavior.
- `storage-config.js` selects demo-mode browser storage.
- `COMPONENTS.md` documents the visible UI and implementation notes.

## Components and effects

| Component / effect | Purpose | Accessibility and performance |
| --- | --- | --- |
| Sticky header, navigation, search | Site navigation and product search | Native links/forms, labels, keyboard focus, compact mobile menu |
| Intro reveal | First-visit brand animation | Session-scoped; respects reduced-motion preference |
| Hero illustration and trust strip | Brand introduction and service messages | Decorative art hidden from assistive technology where applicable |
| Category tiles and product cards | Browse categories and catalog | Descriptive product image alternatives and lazy-loaded catalog images |
| Quantity controls and request list | Collect items and quantities | Accessible button names, input labels, and live status feedback |
| Product detail and gallery | Product information and images | Native buttons, pressed state, descriptive image alternatives |
| Offer cards and countdown | Active/scheduled offer information | Countdown has a label and updates once per second |
| Checkout and business request forms | Prepare quote requests for WhatsApp | Required fields, semantic labels, and inline error/status messages |
| Footer and WhatsApp contact | Company links and contact action | Descriptive accessible name; opens WhatsApp in a separate tab |
| Reveal, spotlight, request-fly animation | Scroll, pointer, and cart feedback | Pointer effects avoid touch; motion is disabled for reduced-motion |
| Light/dark theme and Arabic/English | Display preferences | Persistent browser preference; document `lang` and `dir` are updated |

## Assets, sources, and licensing

- Product, category, and offer photographs use the Unsplash URLs in the site
  data. See the [Unsplash License](https://unsplash.com/license) and confirm
  terms for any new commercial use.
- DM Sans, DM Mono, and Noto Sans Arabic are loaded from Google Fonts; system
  fallbacks remain configured.
- The favicon and image fallback are embedded in `index.html` or `app.js`.
  The WhatsApp contact artwork is embedded in the application bundle. No local
  image files or separate icon package are required.
- Interface icons are bundled from Lucide. WhatsApp's name and mark belong to
  WhatsApp/Meta and identify the contact destination only.

## Performance, storage, and deployment

- The application bundle includes its existing React, router, and icon runtime
  in `app.js`; the browser does not need separate framework or package files.
  There is no runtime build step or external JavaScript dependency.
- Product and offer photos are remote and require an internet connection.
- Catalog data is editable in the single `window.App.CONFIG` block in
  `index.html`. Browser-side changes are saved in local storage and persist
  across visits. Clearing site storage removes those saved changes and restores
  the configured defaults.
- Requests are not transmitted until the customer opens/submits them through
  WhatsApp. There is no online payment or server-side order storage.
- The standalone package does not include a separate web manifest, robots file,
  sitemap, or hosting workflow. Canonical, social, and structured metadata are
  kept in the HTML document.

## Design pass (accessibility, Arabic typography, responsive header)

Changes were made only in `index.html` and `styles.css`; `app.js` and
`storage-config.js` are byte-for-byte unchanged.

- **Contrast:** secondary text now meets 4.5:1 (`--ink-soft`, `--ink-faint`).
  Coral is split into `--accent` (decoration), `--accent-text` (text/icons) and
  `--accent-fill` (behind white text), all at 4.5:1 or better in light and dark.
- **Text size:** every non-decorative text declaration is at least 12px
  (152 declarations raised). The brand sub-line stays 11px as part of the logo.
- **Arabic typography:** letter-spacing and uppercase are disabled in RTL so
  cursive letters stay joined; heading line-height is tuned for Arabic and
  headings use `text-wrap: balance`.
- **Touch targets:** 44px minimum for icon buttons and, on touch screens, for
  quantity/add controls. Footer links have larger hit areas.
- **Header:** tuned so the navigation never overlaps search, brand or actions
  at 1160px and wider, in Arabic and English.
- **Mobile bottom bar:** redesigned as one floating glass dock (frosted blur,
  soft depth, equal-width items, raised pill + accent bar on the current page,
  request counter badge) in light and dark. A small script in `index.html`
  marks the current page because the router does not set `aria-current`.
- **Category tiles:** product count is now separated from the category name.
- **Accessibility:** skip-to-content link, `<main>` receives its id after mount,
  stronger focus ring, `<noscript>` message, global reduced-motion safety net,
  16px form fields on small screens (prevents iOS zoom).
- **Performance:** fonts load through `<link>` instead of a render-blocking
  CSS `@import`.
- **Meta:** light/dark `theme-color`, `og:locale`, `og:site_name`.

Known content items still open: product photos repeat and some do not match
their product (see the delivery notes), `example.com` is still the canonical
URL, and phone/email/address in `window.App.CONFIG.settings` are empty.
