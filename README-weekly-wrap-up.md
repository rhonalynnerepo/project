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

A dedicated landing page whose form is visible on arrival — no popup, no click. Built
with the live site's own CSS, fonts (DM Serif Display / DM Sans), header and footer, so
it matches exactly. Sections: hero + form, what you get, two testimonials, FAQ.

**Status: unfinished.** Paused once the standalone form link turned out to answer the
original question. Before using it:

- [ ] Replace the fallback `<form>` in the `.at-freecard` block with the real GHL embed
      (instructions are in a comment right above it). As written the form is styled but
      submits nowhere.
- [ ] Create the page in GHL at `/weekly-wrap-up` and paste the body in.
- [ ] Point the footer's "The Weekly Wrap-Up" link at it instead of `/events#newsletter`.

`assets/css/site-extracted.css` is the live site's stylesheet, pulled from the home page
and kept only as the reference the page was built against.
