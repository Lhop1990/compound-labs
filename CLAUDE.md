# Compound Labs Website

## What this is
The public marketing site for Compound Labs — a static HTML/CSS/JS site (home, services,
404) with analytics (Plausible + Google Analytics), an SEO setup (sitemap, robots.txt,
OG image), and a contact modal wired to a form-submission endpoint. No framework, no
build step; plain static files served as-is.

## Run / test / deploy
```
# install:  none — no package manager, no dependencies
# dev:      open index.html directly, or `python3 -m http.server` for a local server
# test:     manual — check pages in browser; run Lighthouse for perf/a11y/SEO regressions
# deploy:   push to main; static hosting picks up index.html, services.html, 404.html,
#           robots.txt, sitemap.xml, CNAME directly from repo root
```

## Architecture (~8 lines max)
- `index.html`, `services.html`, `404.html` — the three pages; each independently
  includes its own `<head>` analytics snippets (Plausible + GA) and shared `styles.css`.
- `styles.css` — single global stylesheet for all pages.
- `og.html` / `og-image.png` — source and rendered Open Graph card (1200x630 @2x).
- `email-signature.html` — standalone signature template, not linked from the site.
- `CNAME` — custom domain config for GitHub Pages.
- Analytics: Plausible (event-aware — tracks outbound links, "Open Contact Modal",
  "Submit Contact Form") plus Google Analytics (gtag.js), both firing on page load.

## Gotchas
- GA drops first-party cookies with no consent banner — UK/EU PECR/ePrivacy exposure if
  EU/UK traffic matters; consider a consent banner before relying on GA there.
- Any new page needs its own analytics `<head>` snippet added manually (no shared partial).
- `email-signature.html` is tracked in git but excluded from future changes via
  `.gitignore` — don't assume similar one-off HTML files are automatically ignored.

## Conventions
- Commit after every working milestone; push before ending a session.
- Verify in browser before claiming done — this site has no test suite, so manual/Lighthouse
  checks are the verification step.
