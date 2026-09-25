# Website Improvements: Running List

Ideas and open items for the Power10 Sales site, beyond the initial rebuild. Nothing here is
urgent. Add to it as things come up, and work items in any order. Each one stands alone.

---

## 1. Privacy policy needs a rewrite

The current page is the default WordPress boilerplate. It describes features this site does not
have, which makes it read oddly to anyone who actually reads it:

- Comments and comment forms. There are no comments on the site.
- User registration, login, and password resets. There are no accounts.
- The Gravatar avatar service.
- Uploading media with embedded location data.
- Embedded content from other websites.

It also still says the website address is `http://` rather than `https://`.

**Suggested fix:** replace it with a short, accurate policy. The site is static, has no forms, sets
no cookies, and does no tracking, so the honest version is only a few sentences. A short accurate
policy is better than a long inaccurate one. If a contact form or analytics is added later, update
the policy at the same time.

---

## 2. Google Business Profile

Free, and probably the highest-value item on this list relative to effort.

This is what puts a business in Google Maps and in the panel on the right side of search results.
**It is also what enables Google reviews.** Power10 does not appear to have a profile set up, which
means customers currently have nowhere to leave one.

To set up, you need: business name, category (something like manufacturers' representative or
electronic components supplier), service area (SF Bay Area, Sacramento, Southern California), phone
number, hours, and the website link. Verification is usually by postcard, phone, or email and takes
a few days.

Once it is live, it is worth asking a handful of long-standing customers to leave a review. Reviews
affect both where the business ranks and whether someone decides to call.

---

## 3. SEO basics

Specific gaps in the current site, smallest first:

- **No meta description on any page.** This is the sentence Google shows underneath the link. With
  none, Google writes its own from whatever text it finds.
- **Social preview image only on the home page.** Sharing the About Us or Privacy Policy link on
  LinkedIn produces a bare preview with no image.
- **No `sitemap.xml` and no `robots.txt`.** Both are small files that help search engines index the
  site properly.
- **One image uses a filename as its alt text** (`era_logo_website_blue_II-300x143`). That helps
  neither screen readers nor search.
- **Home page title is "Home-Partners | Power10 Sales".** Something like
  "Power10 Sales | Manufacturers Rep for Electronic Components, Bay Area" describes the business and
  matches what people actually type into Google.
- **Footer still reads © 2023.**

The larger issue: three pages with relatively little text gives search engines very little to work
with. Items 5, 6 and 7 address that, and matter more than any of the fixes above.

---

## 4. AI search visibility (AIO)

People increasingly ask ChatGPT, Claude, Gemini, and Google's AI Overviews for supplier
recommendations instead of scrolling search results. What actually helps:

- **Plain, factual writing.** State what the business does, which lines it represents, and where it
  operates, in direct sentences. AI systems quote clear statements and skip vague marketing language.
- **Structured data** (schema.org Organization or LocalBusiness) describing the business, location,
  contact details, and the lines represented. The old WordPress plugin generated a version of this;
  it was removed during the rebuild because it was full of stale WordPress data. A clean hand-written
  one would be an improvement on what was there.
- **FAQ content** (item 6) is unusually effective here, because a question-and-answer format maps
  directly onto how people ask these tools things.
- **Consistent listings elsewhere** (Google Business Profile, the ERA directory, partner websites) so
  the AI has corroborating sources for the same facts.

Worth being straight about this: it is less predictable than traditional SEO, and nobody can
guarantee placement in AI answers. The good news is the work overlaps almost entirely with regular
SEO and good content, so it is not a separate project competing for budget.

---

## 5. More pages

Roughly in order of value:

- **One page per partner line** (Winonics, GCT, METALfx, KTP). This is the strongest item on the
  list. It gives each partner real estate, it lets someone searching "GCT connectors rep California"
  actually find the site, and it multiplies the amount of indexable content. It is also an easy sell
  to the partners themselves.
- **Line card or capabilities page**, possibly with a downloadable PDF version.
- **Contact page.** Phone and email currently live only on the About Us page.
- **Territories served**, if the coverage area is a common question.

---

## 6. FAQs

Strong candidates, based on what a prospective customer would want to know:

- What does a manufacturers' rep do, and what does it cost me to work with one?
- Which territories do you cover?
- Which product categories do you represent?
- Can you support prototypes and low-volume runs, or only production quantities?
- How do I request a quote?
- What are typical lead times?

These earn their place twice over: they answer real questions for customers, and they feed both
search and AI systems in exactly the format those systems prefer.

---

## 7. More text on the existing pages

The About Us page is two short paragraphs. Things that would strengthen it: how long Power10 has
been doing this, which industries it serves, what working with the company is actually like, and why
these four lines in particular. This is also the cheapest way to improve search performance.

- **Add pictures from my past rowing experience.** Reminder to pull photos and work them into the
  About Us page.

---

## Other suggestions

- **Contact form.** Currently the only options are phone and email. A form captures people who will
  not pick up the phone. Note that a static site cannot process a form by itself, so this needs a
  third-party service, and that would be the site's first external dependency. Worth doing, but it is
  a real tradeoff rather than a free win.
- **Analytics.** There is none at all right now, so there is no way to know which pages people read
  or what they search for to arrive. A privacy-friendly option avoids cookie-banner obligations.
- **Copyright year.** Update it, and consider making it update itself.
- **Enforce HTTPS.** Turn this on in the GitHub Pages settings once the domain is connected and the
  certificate has been issued.
- **Contrast check.** The accessibility basics are in place. The gold-on-black text is worth checking
  against contrast guidelines, particularly at smaller sizes.
- **Logo sizing.** The METALfx logo renders about 510px wide while the other three render 300px. It
  was like that on the old site too, so it is cosmetic rather than a defect.

---

## How to use this list

Add items whenever they come up. When you want to act on one, tell Claude Code which item you mean
and it can do the work. Delete items once they are done, or move them to a "Done" section if it is
useful to keep the history.
