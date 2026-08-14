# Building a developer page that holds up

Written for the Boxstack Play Store release. Two jobs, and they are not the same job:

1. **Satisfy Play's requirements.** A privacy policy URL, a support email, a developer name.
   These are checked. Getting them wrong blocks the listing.
2. **Convince a human who looks you up.** A player who taps *Developer website*, or anyone
   deciding whether this is a real operation. This is the profile page.

Job 1 is a blocker. Job 2 is polish. Do them in that order.

---

## 1. What Play actually requires

**Google does not read your GitHub profile.** Account verification is identity documents —
and a D-U-N-S number if you register as an organisation. No README changes that. What the
Console does ask for:

| Field | Where | Required? | Notes |
|---|---|---|---|
| Developer name | Account | Yes | Public on every listing. Hard to change later — pick deliberately. |
| Contact email | Account | Yes | Verified. Not necessarily the one shown publicly. |
| Contact phone | Account | Yes | Verified by SMS. Never shown publicly. |
| Physical address | Account | Yes | **Public on the listing** for personal accounts in most regions. |
| Website | Account | No | Public. Empty here is a small credibility cost. |
| Support email | Per app | Yes | Public on the listing. |
| **Privacy policy URL** | Per app | **Yes, for Boxstack** | See below. |

### The privacy policy

Every app on Play needs one, even an app that collects nothing.

`docs/SHIP-DESIGN.md:486` framed this as an ads problem — but **BoxStacker v1 has no ads and
collects nothing at all.** Verified against the source: the manifest declares *no Android
permissions whatsoever*, including no `INTERNET`, and the only dependencies are AndroidX
(Compose, activity, core, datastore, lifecycle). There is no AdMob, no billing, no Firebase and
no analytics. `AdPolicy` is pure cadence arithmetic with no SDK behind it yet.

That is a strong position, and it is worth stating plainly on the listing:

- The Data safety form is a clean **No data collected / No data shared**, which earns the
  *No data shared with third parties* badge.
- The claim "cannot send data anywhere" is **structural, not a promise** — there is no network
  permission to abuse. Very few games can say that truthfully.

**This becomes false the moment AdMob is added.** The policy and the Data safety form both have
to be rewritten before that build is submitted. Requirements Google enforces:

- **Publicly reachable** — no login, no interstitial, no `noindex` gate.
- **Stable** — the same URL for the life of the app. Not a Google Doc link, not a Notion page
  you might reorganise, not a URL with a session token in it.
- **App-specific** — it must name Boxstack and describe what Boxstack does, not be a generic
  template about a company.
- **Matches the Data safety form** — a mismatch between the form and the policy is a common
  rejection, and it is the kind that costs a review round trip.
- **Covers the ad SDK, once there is one** — what AdMob collects, that it is used for
  advertising, how the consent mechanism (UMP) works, and how to change that choice.

GitHub Pages is an acceptable host. A repo serving `https://<user>.github.io/boxstack/privacy`
satisfies every bullet above and costs nothing.

**Do not ship a policy you have not read.** Generator output frequently claims collection you
do not do, or omits the ad SDK entirely — either way the Data safety form disagrees with it.

---

## 2. Where the page should live

Three options, increasing effort:

**A. Profile README only.** The `jjpatric9/jjpatric9` repo. Renders at
`github.com/jjpatric9`. Zero infrastructure. But a GitHub URL in the Play *Website* field is
a slightly odd look for a game studio, and it cannot host the privacy policy at a stable
non-GitHub-looking path.

**B. Profile README + GitHub Pages site.** Recommended. The Pages site is the *Website* field
and hosts `/privacy` and `/support`; the profile README is the developer-facing face. Free,
and a custom domain can be pointed at it later without changing the structure.

**C. GitHub organisation.** If the front-facing identity is *TallmanGames* rather than a
person, an org gives you `github.com/tallmangames` with repos owned by the studio. Org profile
READMEs live in a `.github` repo at `profile/README.md`. More convincing for a studio identity,
and slightly more to maintain.

These compose — an org can have a Pages site too.

---

## 3. What makes a profile page good

### Above the fold

A reader decides in about five seconds. The first screenful needs: **who you are, what you
make, one link that works.** Everything else is below that line and optional.

### Be concrete, not adjectival

"Passionate developer with a love for clean code" says nothing and reads as filler. Specifics
about real work carry weight because they cannot be bluffed:

> **Boxstack** — Android stacking game. Kotlin, Jetpack Compose. Game rules live in a pure-JVM
> module with no Android dependencies, so the whole ruleset is testable without an emulator.
> Balance tuning is driven by a soak suite that plays hundreds of complete games with scripted
> bots.

That paragraph is more persuasive than any badge, and every clause is true.

### Show the thing

One screenshot or a short GIF of Boxstack running outperforms the entire rest of the page. A
games developer whose page contains no game footage is the single most common own-goal here.

### Repositories, and what your evidence actually is

Pinned repos are the most-looked-at part of a profile — for a developer building peer
credibility or job-hunting. **That is not this situation**, and the distinction matters:

> For a Play Store application, **the live listing is the evidence**, not a source repo.
> Essentially no commercial game ships its source. A studio profile that links to a store page
> and a working site, with no public source, is entirely ordinary and implies nothing.

**Closed-source is the default, not a hedge.** Declining to publish source is a normal business
decision that says nothing about how something was built. It is not the same act as publishing
a doctored history, and should not feel like one.

So the public-presence need is met by the **site repo** — genuinely public, genuinely active,
and it does the whole job of "this account is real." Boxstack itself stays private.

The one thing to avoid: **never link to a private repo from a public page.** It 404s for every
visitor, which is worse than not linking at all. Check every link while signed out.

### Contact that matches

The email on your profile, the Play Console support email, and the address in the privacy
policy should be the same string. Three different addresses across three surfaces is exactly
the inconsistency that makes a careful reader suspicious.

---

## 4. What to avoid

These are the things that are *meant* to signal legitimacy and do the opposite.

- **Stats widgets, streak counters, trophy walls.** On an account with 0 public repos and 0
  followers they render actual zeros — an automated display of having done nothing. Even on a
  busy account they are pattern-matched as decoration and skimmed past.
- **Icon walls of every technology you have touched.** Twenty logos including things used once
  devalues the ones you actually know. List what Boxstack is built in; stop there.
- **Claimed experience, employers, titles or credentials that are not yours.** Beyond the
  ethics: it is checkable, it is inconsistent with a 2023 account and one app, and being caught
  is far more damaging than being modest. Everything on the page should survive someone
  deciding to verify it.
- **Visitor counters and "profile views" badges.** They read as 2012.
- **"Currently learning" lists.** Nobody is persuaded by intentions. Ship notes persuade.
- **Links to private repos.** They 404 for every visitor. Check every link while signed out.
- **An animated typing banner.** It delays the information the reader came for.

The general rule: **anything automated that displays a number about you is a liability while
the numbers are small.** Prose about real work has no such floor.

---

## 5. Mechanics

**Personal profile README**
- Repo name must exactly equal the username: `jjpatric9/jjpatric9`.
- Must be **public**. A private profile repo renders nothing.
- `README.md` at the repo root.
- Renders at `github.com/jjpatric9`, above the pinned repos.

**Organisation profile README**
- Repo named `.github` inside the org.
- File at `profile/README.md` — not the root.

**Both**
- GitHub-flavoured Markdown. Raw HTML is allowed but scripts and most styling are stripped.
- Images must be absolute URLs or committed to the repo. A relative path to a file that is not
  in *this* repo is a broken image.
- Dark mode exists: a screenshot with a white background on a dark-themed profile glares.
  `<picture>` with `prefers-color-scheme` handles it if you care.

**GitHub Pages**
- Settings → Pages → deploy from branch, or an Actions workflow.
- Serves at `https://<user>.github.io/<repo>/`, or the apex if the repo is named
  `<user>.github.io`.
- A custom domain is a `CNAME` file plus a DNS record, and can be added later without breaking
  the `github.io` URLs.

---

## 6. Consistency check before submitting

One name, one email, one site, everywhere:

- [ ] Play Console developer name — matches GitHub display name (or is deliberately different)
- [ ] Play Console website field — resolves, is public, mentions Boxstack
- [ ] Play Console support email — same as the profile and the privacy policy
- [ ] Privacy policy URL — loads signed out, in a private window, on mobile
- [ ] Privacy policy names Boxstack, AdMob, and the consent mechanism
- [ ] Data safety form agrees with the privacy policy, line by line
- [ ] Every link on the profile works while signed out
- [ ] No link points at a private repo
- [ ] Screenshots render on both light and dark themes
- [ ] App name on the page matches the Play listing exactly

---

## 7. Decisions taken

| Question | Decision |
|---|---|
| Front-facing identity | **TallmanGames**, with Joshua Patrick named behind it |
| Where the page lives | Profile README + GitHub Pages site |
| Boxstack repo | **Stays private** — normal for a commercial game |
| AI tooling | Stated as method, not confession: *"I build with AI tooling"* |
| Play account | **Personal + virtual mailbox address** |
| Store name | **BoxStacker** (matches `applicationId = com.boxstacker.app`) |

### The address decision, and its one open question

A **personal** Play account publishes the developer's address on every listing, worldwide, and
Play listing data is widely scraped and mirrored. A virtual mailbox (UPS Store, Anytime Mailbox,
iPostal1 — all operate in Canada) gives a street-format address for roughly $15–30 CAD/month. A
bare Canada Post PO Box is usually rejected; Google wants street format.

**Confirm before paying for a mailbox:** Google's verification may require the account address
to correspond to your government ID, which a virtual mailbox would not satisfy. That requirement
has changed several times since 2023. Start the sign-up, reach the verification step, and read
what it actually asks for before committing money.

If it turns out the address must match your ID, the fallback is an **organisation** account —
free D-U-N-S number, ~1–2 weeks, publishes a business address instead, and makes the developer
name legitimately *TallmanGames*.

### Naming inconsistency to reconcile

The store name is **BoxStacker** and `applicationId` is `com.boxstacker.app`, but the repo,
`CLAUDE.md` and every doc say **Boxstack**. The site and profile use *BoxStacker* throughout.
Worth eventually settling on one name in the project docs too.

---

## 8. Order of work

1. **Get a gameplay GIF off a real device.** Highest-value missing asset, and only you can make it.
2. Publish the site — `index.html`, `privacy.html`, `support.html` live at a stable URL.
3. Start Play Console sign-up; check what the verification step demands before buying a mailbox.
4. Sort the address, then complete account verification.
5. Data safety form — declare **No data collected**, and check it against `privacy.html` line by line.
6. Profile README: drop in the GIF and the store link once both exist.

Steps 2–5 are the release. Steps 1 and 6 are the credibility.
