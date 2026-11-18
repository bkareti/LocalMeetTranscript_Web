# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Static marketing site for MeetQyl (a private, on-device meeting-notes app for Mac), served at https://www.meetqyl.com/. Plain HTML, CSS and vanilla JS. There is no build step, package manager, linter, test suite or git repo.

## Running locally

Open `index.html` directly, or serve the folder: `python3 -m http.server 8000`.

## Structure

- `index.html`, `privacy.html`, `support.html`: three hand-written pages. Header, nav and footer are duplicated in each file, so a nav or footer change must be made in all three.
- `assets/css/styles.css`: the only stylesheet. Dark theme is the default in `:root`. Light theme comes from a `prefers-color-scheme: light` media query (no manual toggle).
- `assets/js/main.js`: mobile nav toggle and scroll-reveal only. Keep it free of network requests and tracking, since the site's privacy claims depend on this.
- `assets/img/`: images are paired by size (`-800`/`-1600`, `-64`/`-128`) and light/dark (app icons). Pages use `<picture>` with a `prefers-color-scheme` source for the icons.
- `robots.txt`, `sitemap.xml`: use absolute `www.meetqyl.com` URLs. Update `lastmod` in the sitemap when a page changes. A new page needs a sitemap entry, a canonical link and OG/Twitter meta like the existing ones.

## Conventions to preserve

- Progressive enhancement: `<html>` gets a `js` class from an inline script before the stylesheet applies, and `.reveal` elements only hide when `js` is set. Reveal is skipped under `prefers-reduced-motion`.
- Accessibility is built in (skip link, `aria-*` on the nav toggle, `Escape` closes the menu). Keep it when editing markup.
- The iPhone section is a teaser only: no link and no download.
- The download CTA (`#download`) is the target of the "Get MeetQyl" nav button.
- Privacy copy (no account, no tracking, on-device transcription, one-time speech-model download after confirmation) must stay consistent across `index.html`, `privacy.html` and `support.html`.

## Related skill

`build-test-dmg` builds time-limited test DMGs of the app. It is about the app, not this site.
