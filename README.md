# a3quumsolutions.com

The A3Q website. Three self-contained pages: all CSS is inline, the logo is inline SVG,
and the favicon is a data URI, so there are no asset paths to break.

    index.html            served at /
    privacy/index.html    served at /privacy
    terms/index.html      served at /terms
    og-card.png           the social share card, 1200x630
    CNAME                 a3quumsolutions.com — do not edit
    .nojekyll             tells Pages to serve these files as they are

`assets/` holds twelve images from the previous investor page. Nothing here references
them. They are harmless to leave and safe to delete.

## How it deploys

GitHub Pages, deploy from a branch: **`main`, `/ (root)`**. There is no build step and no
staging branch. **A commit to `main` goes live.** Review the diff in GitHub Desktop before
committing, not after.

`CNAME` is what holds the custom domain. Changing or removing it drops the domain and the
site falls back to the github.io address.

## The ground is dark

Graphite #0D0D0D is the ground on all three pages. Two consequences worth knowing:

**There is one orange.** Orange Deep #C93C0A measures 3.83:1 on graphite and fails, so it
is absent. A3Q Orange #FF5A1F is 6.23:1 on graphite and passes at any size, which is why a
dark base needs only one. The `--a3q-orange-deep` token still exists and now resolves to
#FF5A1F, so nothing downstream breaks.

**There is a new token.** `--a3q-raised: #161616`, the surface for the sections that were
Light Gray. The palette in 07 has no dark raised surface, so this is a **proposed addition
to the design system**, not something 07 currently sanctions. 07 Section 04 still names
light as the default surface and needs amending to match.

The hero is graphite, not orange. Orange is the accent: the rule, the mono line and the
watermark. The closing invite section is the one full-orange surface on the page.

## Editing

Colour and type values come from the A3Q Design System (07 in the brand kit) and are
declared once as CSS custom properties at the top of each file's `<style>` block. Change
them there, not inline. The two legal pages share a shell with each other but not with
`index.html`, so editing one does not update the other.

## Google Tag Manager

Container **GTM-5SG8HF32**, installed in two halves on every page, carrying the same ID:

1. The loader in `<head>` — `var GTM_ID = "GTM-5SG8HF32";`
2. The `<noscript>` iframe immediately after the opening `<body>` tag

Emptying the string in the loader switches tracking off: nothing loads and no cookies are
set. Remove the noscript iframe at the same time, or visitors with JavaScript off are
still tracked. GA4 property `G-WLTZVS6ESM` fires through the container.

## The contact address

`InvestorOpp@a3quumsolutions.com`. It is **assembled by the browser at load time**, so
scrapers reading the page source do not find it. To change it, edit the `P` array in the
script near the bottom of each file:

    var P = ['InvestorOpp','a3quumsolutions','com'];

and the readable fallback in the markup, which is what a visitor with JavaScript off sees:

    <span class="a3qmail">InvestorOpp [at] a3quumsolutions [dot] com</span>

A `data-label` attribute on that span renders a word instead of the address — the homepage
uses `data-label="Email us"`. Without it the address itself is the link text, which is what
the legal pages want. Do not replace either with a plain `mailto:` link.

## The share card

`og-card.png`, 1200x630, referenced by absolute URL from all three pages. Rebuild it from
`build_og.py` in the site source rather than editing the PNG. If the tagline in the page
title changes, change it here too — they are the same line and a link preview showing the
old one is the kind of thing nobody notices for months.

LinkedIn caches previews hard. After changing this file, run the URL through LinkedIn's
Post Inspector to force a refresh, or the old card keeps appearing.

## Section ids, for measurement

Every section on `index.html` carries an id, so GTM's built-in Element ID variable names it
without a custom variable:

    hero  why  separation  origin  companies  how  contact

`why`, `companies`, `how` and `contact` are also the header nav anchors. Do not rename
those four without changing the nav.

## Motion

Every section animates on scroll, gated behind `prefers-reduced-motion` and behind a `.js`
class added to `<html>` in the head. A reduced-motion setting or a JavaScript failure
leaves the page static and fully readable. The legal pages carry no animation.

## Notes on content

The entity is **Aequum Solutions, Inc.**, a Delaware corporation qualified in Alabama
(Alabama SOS entity 001-272-392). `/terms` is governed by Alabama law with venue in
Jefferson County, matching the VoteCivic Terms of Service.

The records paragraph in the "Dedicated companies" section was confirmed as accurate by
Adil Patel on 16 September 2026.

The three-beat on this page is ENGINEER. STEWARD. DELIVER. The brand kit and the approved
look board still say BUILD. LAUNCH. IMPACT. Update 04 Brand Messaging so the two agree
before anyone builds collateral from the kit.
