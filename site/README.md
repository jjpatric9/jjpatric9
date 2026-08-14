# TallmanGames site

Static pages for the Play Store listing's **Website**, **Privacy policy** and **Support** fields.
No build step, no dependencies — four files, plain HTML and one stylesheet.

| File | Purpose |
|---|---|
| `index.html` | Landing page. Goes in the Play Console **Website** field. |
| `privacy.html` | Privacy policy. Goes in the per-app **Privacy policy** field. Required. |
| `support.html` | Support and FAQ page. |
| `style.css` | Shared styling. Light and dark, no web fonts, no external requests. |

All links between pages are **relative**, so the site works unchanged whichever way it is hosted.

## Publishing it

**Option A — a user site at the apex URL (recommended).** Create a public repo named exactly
`jjpatric9.github.io`, copy these four files to its root, push, and enable Pages in
Settings → Pages → deploy from `main` / root. Gives:

- `https://jjpatric9.github.io/`
- `https://jjpatric9.github.io/privacy.html`
- `https://jjpatric9.github.io/support.html`

**Option B — serve from this repo.** Settings → Pages → deploy from `main` / `/site`. Gives
`https://jjpatric9.github.io/jjpatric9/privacy.html` — works fine, but a longer, less tidy URL
to hand to Play.

## Before submitting to Play

- [ ] Replace the `<!-- SCREENSHOT -->` comment in `index.html` with a real gameplay GIF
- [ ] Replace the `<!-- STORE LINK -->` comment in `index.html` once the listing is live
- [ ] Update the "Last updated" date in `privacy.html` if the policy changes
- [ ] Open every page signed out, in a private window, on a phone
- [ ] Check the policy against the Data safety form line by line

## When ads are added

`privacy.html` currently states, accurately, that BoxStacker collects nothing and has no network
access — the app requests **no Android permissions at all**, so this is verifiable rather than
merely asserted.

Adding the AdMob SDK breaks every one of those claims at once. The policy must be rewritten to
cover what AdMob collects, the UMP consent flow and the advertising ID, **and** the Data safety
form updated to match, **before** that build is submitted. A policy that disagrees with the Data
safety form is a standard rejection.
