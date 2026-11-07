# 2021.trondheimdc.no

A static archive of the TDC Community Week 2021 website (25th-28th October 2021).

This is a **static archive** of that website, kept as a historical record. It is not the live
conference site and nothing here is maintained.

The original was a Laravel/Livewire application. This copy is plain HTML, CSS and JS with
no build step and no external requests. It is served by nginx on worldwide.trondheimdc.no, and
deployed from `main` by GitHub Actions. See [docs/deploy.md](docs/deploy.md).

## Provenance

- `index.html`: Internet Archive capture of 2021-11-28 17:12:33 UTC
  (https://web.archive.org/web/20211128171233/https://2021.trondheimdc.no/).
  Livewire scripts and the CSRF token were removed, asset URLs made relative.
- `css/app.css`: original stylesheet (Internet Archive, 2022-03-19). URLs made relative and
  the Google Fonts `@import`s replaced by self-hosted copies in `css/fonts.css` and `fonts/google/`.
- `js/bootstrap.bundle.min.js`: Bootstrap 5.0.2 (with Popper), the same version as the original
  `app.js` bundle. The original 1.2 MB webpack bundle also contained Alpine, axios, lodash and jQuery 3,
  none of which the page uses, so it was replaced by the official release. The 2021-11 page did not
  load any Bootstrap JS, so its mobile menu did not open. It is included here so it works.
- The inline script in `index.html` that swaps the hamburger icon was rewritten from jQuery 1.7.1 (loaded
  from Google's CDN in the original) to plain JavaScript with identical behaviour.
- `robots.txt`: the original (allows everything).
- `img/`: original assets, untouched (including the 1.2 MB hero image).
- `fonts/vendor/`: original Font Awesome 5.15.4 fonts. Only `woff2` and `woff` are kept; the `eot`, `svg` and
  `ttf` fallbacks for obsolete browsers were removed together with their `@font-face` entries.

## Intentional changes from the archived page

- The Code of Conduct named an individual with a private phone number as contact. That is
  replaced by connect@trondheimdc.no.
- Links to meetup.com, Facebook, Eventbrite and Hoopla are unchanged. They are third-party pages from 2021 and
  may change or disappear.
