# Power10 Sales website

Static site on GitHub Pages at www.powertensales.com. Rebuilt from a WordPress/Beaver Builder
site; the raw wget mirror is committed in `_source/` as reference material.

## Hard rules

- **No external requests.** Fonts and icons are self-hosted. No `fonts.googleapis.com`, no CDN,
  no analytics unless asked. Verified by rendering with external DNS blackholed.
- **No `wp-content`, `wp-includes`, or old-host URLs in deployed files.** `_source/` is the only
  place those may appear.
- **All paths are root-relative** (`/assets/...`). Because of this, opening a page as `file://`
  shows an unstyled mess. Always preview over HTTP.
- **Never deploy or edit `_source/`.** Reference only.
- **Keep `CNAME` and `.nojekyll` at the repo root.** `CNAME` binds the custom domain;
  `.nojekyll` stops GitHub Pages running Jekyll over the files.

## Structure

| Path | Loaded by |
|---|---|
| `index.html`, `about-us/index.html`, `privacy-policy/index.html` | the three pages |
| `assets/css/site.css` | all pages |
| `assets/js/site.js` | all pages |
| `assets/js/layout-home.js` | home only |
| `assets/js/layout-about.js` | about-us only |

`site.js` = jQuery 3.7.1 + throttle/debounce + `themeopts` + Beaver Builder theme JS (mobile nav,
fixed header, scroll-to-top). The `layout-*.js` files drive the parallax row background.
privacy-policy loads neither, which matches the original site.

## site.css cascade order — do not reorder

`@font-face` → Font Awesome → Dashicons subset → Beaver Builder layout → theme base → skin →
child theme. The skin defines the black/gold palette and the Cabin / Archivo Black assignments,
and must stay after base.

## Traps

**1. Per-page CSS is merged into one file.** The Beaver Builder layout CSS originally loaded only
on builder-built pages. It ends with `.page .fl-post-header{display:none}`. privacy-policy is a
block-editor page that *shows* its title header, so that rule is scoped to `.fl-builder.page` — a
body class present on home and about-us but not privacy-policy. **Do not unscope it.** Unscoping
hides the "Privacy Policy" heading and shifts the whole page up.

**2. Icons are subsetted.** Of ~1458 Font Awesome rules, only `.fa-phone-alt`,
`.fa-envelope-open-text` and `.fa-chevron-up` remain. `fa-solid-900.woff2` still contains every
solid glyph, so adding another `fas` icon is one CSS line. `fab` / `far` icons need their webfont
copied from `_source/.../fontawesome/5.15.4/webfonts/` plus an `@font-face`. See the comment above
the Font Awesome section in site.css.

**3. The email icon is Dashicons, not Font Awesome** (`dashicons-email-alt`, on home and
about-us). Its font is an inline base64 WOFF inside site.css — nothing external.

**4. `themeopts` must be defined before the theme JS runs.** It is read unguarded. It sits at the
top of site.js; do not move it below the theme block.

**5. jQuery Migrate, magnific popup and fitVids were removed** after confirming nothing calls
them. If a future feature needs a lightbox, re-add magnific popup rather than assuming it is there.

## Images

One file per image at its displayed size, with two deliberate exceptions:

- **GCT logo** uses `srcset` (300w + 500w) because the retina file is 29KB vs 6KB.
- **KTP logo** ships a single 508px file — it is 2,740 bytes, smaller *and* sharper than its own
  300px version (7,883 bytes), so one file is optimal on every screen.

Keep the `width`/`height` attributes. With `height:auto` in the theme CSS, the `width` attribute
is the presentational hint that holds each logo at its intended display size.

## Verifying a change

Do not verify by reading files alone. Serve and render:

```
python3 -m http.server 8000
```

Load all three pages, confirm no 404s and no external requests. Reference point: about-us and
privacy-policy render byte-identical to the live WordPress site; home differs only in the KTP
logo's anti-aliasing, which is intentional.

## Licensing

Beaver Builder CSS/JS and Dashicons are GPLv2 (inherited from the original site). Font Awesome 5
Free, Bootstrap, html5-boilerplate, jQuery, Cabin and Archivo Black are permissive. The license
comments in site.css are required — leave them in place.
