# Power10 Sales website

Static site on GitHub Pages at www.powertensales.com. Rebuilt from a WordPress/Beaver Builder
site; the raw wget mirror is committed as `_source.zip` as reference material. It is a zip
rather than a folder because 32 of its files contain `?` or `:` in the filename, which
Windows forbids; checking those out breaks `git clone` on Windows entirely. Unzip it locally
if you need it (the unzipped folder is gitignored). Do not commit it back as loose files.

## Hard rules

- **No external requests.** Fonts and icons are self-hosted. No `fonts.googleapis.com`, no CDN,
  no analytics unless asked. Verified by rendering with external DNS blackholed.
- **No `wp-content`, `wp-includes`, or old-host URLs in deployed files.** `_source/` is the only
  place those may appear.
- **All paths are root-relative** (`/assets/...`). Because of this, opening a page as `file://`
  shows an unstyled mess. Always preview over HTTP.
- **Never deploy or edit `_source.zip` or an unzipped `_source/`.** Reference only.
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
copied out of `_source.zip` (`.../fontawesome/5.15.4/webfonts/`) plus an `@font-face`. See the comment above
the Font Awesome section in site.css.

**3. The email icon is Dashicons, not Font Awesome** (`dashicons-email-alt`, on home and
about-us). Its font is an inline base64 WOFF inside site.css — nothing external.

**4. `themeopts` must be defined before the theme JS runs.** It is read unguarded. It sits at the
top of site.js; do not move it below the theme block.

**5. jQuery Migrate, magnific popup and fitVids were removed** after confirming nothing calls
them. If a future feature needs a lightbox, re-add magnific popup rather than assuming it is there.

## Partner section (home page)

One nested column group per partner, logo left and copy right, in this DOM order:
**Winonics, GCT, METALfx, KTP**. Earlier the site put GCT and KTP in a single shared group
(logos stacked in one column, copy in the other), which made each logo's vertical position
depend on the neighbouring text length. One group per partner removes that coupling, so adding
or reordering a partner is a self-contained edit.

To add a partner, copy an existing group and give the new column/module nodes fresh ids, then add
their rules to site.css. **Check the brace depth before inserting CSS**: the `color` and
`font-size` rules for these modules sit at top level, but the matching `margin-top` rule lives
inside `@media ( max-width: 768px )`. Pasting a colour rule into that media block leaves the copy
white-on-white on desktop, which is invisible against the section's white background and easy to
miss. Verify with a render, not by reading the file.

Node ids added after the original build: `wnc4ph8x2v6t` / `wnc4tx9k3m7r` (Winonics photo/text) and
`ktp5gr2n8w4d` / `ktp5cl6y1j3s` / `ktp5cl7b9q2f` (KTP group and its two columns). Winonics reuses
the two empty spacer columns `txo9d8a3qr0h` and `nkelf1tq3c5m` that the original layout left behind.

Known cosmetic quirk, carried over from the original site: the METALfx logo renders roughly 510px
wide while the other three render 300px, because it is a `size-full` image bounded only by its
column. Left as-is to match the original.

## Images

One file per image at its displayed size, with these deliberate exceptions:

- **GCT logo** uses `srcset` (300w + 500w) because the retina file is 29KB vs 6KB.
- **Winonics logo** uses `srcset` (300w + 600w) for the same reason. The supplied artwork was
  3300x2550 with the logo floating in transparent padding; it is trimmed to its alpha bounding
  box (2416x592, ratio 4.08:1) and rendered 300px wide to sit alongside the other partner logos.
- **KTP logo** ships a single 508px file — it is 2,740 bytes, smaller *and* sharper than its own
  300px version (7,883 bytes), so one file is optimal on every screen.

The rule of thumb: offer two sizes when the retina file is meaningfully heavier; ship one when the
larger file is already small.

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
