# WARP.md

This file provides guidance to WARP (warp.dev) when working with code in this repository.

Project summary
- Static single-page site. No build step, package manager, linter, or tests configured.
- Entry point: index.html (Tailwind via CDN, small inline CSS, vanilla JS for UX behaviors).

Common commands
- Open directly in a browser (quick preview):
  - Windows: start index.html
  - macOS: open index.html
  - Linux: xdg-open index.html
- Run a local static server (recommended to exercise hash navigation and History API):
  - Python: python -m http.server 8000  → http://localhost:8000/index.html
  - Node: npx serve -l 8000 .          → http://localhost:8000/
- Lint/tests: none configured.

High-level architecture
- Styling: Tailwind CSS via CDN (<script src="https://cdn.tailwindcss.com"></script>), with a small inline tailwind.config extension (fonts, gradient brand colors, custom boxShadow) and a minimal <style> block (gradient button, star rating, smooth scroll).
- Head: SEO meta (title/description/keywords/geo), Open Graph tags, Google Analytics (gtag) initialization.
- Layout (big picture):
  - Header with background image overlay → Top bar/logo → Sticky nav.
  - Hero section with CTA buttons.
  - Main content: Reviews (3 product cards), Comparison table, Guide (informational SEO content), Recipes (3 cards that open inline modals), Affiliate disclaimer, Subscribe form (no backend), Contact form (no backend).
  - Footer with links and social icons.
- JavaScript (inline at document end):
  - Smooth in-page scrolling for hash links, intentionally skipping modal links.
  - Hash-based modal open/close (post-smoothies, post-morning, post-keto) with History API integration; deep links open the targeted modal on load.
  - Scroll-to-top button toggled after ~400px scroll; smooth scroll to top on click.
- External assets/services: Unsplash-hosted images, ClickBank affiliate links (rel="nofollow noopener"; target _blank), Google Analytics (gtag).

Repo-specific notes for agents
- Preserve affiliate link attributes (rel="nofollow noopener" and target) and existing IDs/hrefs used for in-page navigation and modals.
- Modals rely on matching IDs (post-smoothies/morning/keto) and data attributes (data-modal-link, data-close-modal, data-overlay); keep these intact when editing or duplicating patterns.
- Prefer Tailwind utility classes; only add to the small <style> block if absolutely necessary. Avoid introducing a bundler/tooling unless explicitly requested.
- If adding nav items or sections, ensure href="#section" matches the section id to retain smooth scrolling and sticky-nav behavior.
- .vercel/ is gitignored; suitable for static hosting. No Vercel config file is present in the repo.
