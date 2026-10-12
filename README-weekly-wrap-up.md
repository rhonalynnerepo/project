# The Weekly Wrap-Up — links & page

## The standalone form link (this is the one to share)

```
https://links.assatathomas.com/widget/form/wDko2EkmGCWPQJcqvku9
```

Verified live: HTTP 200, renders First Name + Email + Subscribe. This is the same GHL
form (id `wDko2EkmGCWPQJcqvku9`) already embedded in the site's popup, so submissions
flow into the same place. Use it for link-in-bio, DMs, texts, QR codes.

## Why a link was needed

On assatathomas.com the Weekly Wrap-Up form lives inside a `<dialog id="atNewsletter">`
popup, opened by the announcement bar, any Subscribe button, and any link to
`#newsletter`. A popup has no URL of its own, so `/#newsletter` and `/events#newsletter`
only scroll to a section containing a *button* — the form appears after a click. The
`#newsletter` section itself has a benefits card, not an inline form.

Note: a leftover "paste your GHL form embed here" comment sits above the popup's iframe.
The iframe underneath it is real and working — the comment is just stale and can be
deleted.

## Option: a branded link that auto-opens the popup

Roughly five lines, added to the site's existing script block, would make
`assatathomas.com/?subscribe=1` open the popup on load:

```js
if (new URLSearchParams(location.search).has('subscribe')) {
  var d = document.getElementById('atNewsletter');
  d && (d.showModal ? d.showModal() : d.setAttribute('open',''));
}
```

Branded, but heavier to load than the raw form link. Not yet applied to the live site.

## `pages/weekly-wrap-up.html`

A dedicated landing page whose signup card is a visual match for the popup: the same
`#faf5f0` cream, 10px radius, 520px cap, clamp padding, shadow, eyebrow, DM Serif title,
body copy and fine print — all values lifted from the live site's own `.atnl-*` rules.
It sits on an espresso band so it reads like the popup over its dimmed backdrop. There is
no close button, since there is nothing to close on a page.

The form is the **real GHL embed** (`wDko2EkmGCWPQJcqvku9`), the same one the popup uses,
so submissions land in exactly the same place. `form_embed.js` is included to size the
iframe to its content.

Below the card: what you get (3-up), two testimonials, and a four-item FAQ — all in the
site's own classes, with the live header and footer.

Verified by rendering in Chromium at 1291px and at 390px: form loads, sections render,
no horizontal overflow on mobile.

### To publish it

- [ ] Create a page in GHL at `/weekly-wrap-up` and paste in everything from `<header>`
      through `</footer>`. The site-wide CSS already covers the `at-*` classes; the
      `ww-*` block in this file's `<style>` is the only addition needed.
- [ ] Keep `<script src="https://links.assatathomas.com/js/form_embed.js"></script>` —
      without it the iframe will not resize to its content.
- [ ] Point the footer's "The Weekly Wrap-Up" link at `/weekly-wrap-up` instead of
      `/events#newsletter`.
- [ ] If you ever paste this body onto a page that also carries the popup, change the
      iframe's `id` so it does not collide with the popup's.


`assets/css/site-extracted.css` is the live site's stylesheet, pulled from the home page
and kept only as the reference the page was built against.
