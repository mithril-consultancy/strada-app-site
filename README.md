# Strada app site

The public home for the **Strada** app (iOS `inc.ludus.strada-agents`, Android
`inc.ludus.strada.agents`):
basic app info, the support contact, and the privacy policy the store listings
point at.

Static site, no build step, no backend, no analytics. The imagery is drawn
live on canvas by the site's own engine; the app footage is real capture.

## Deploy (Vercel)

From the repo root:

```
vercel deploy --prod --yes
```

Notes for whoever hosts it:

- `.vercelignore` whitelists `assets/` file by file. A newly referenced asset
  needs its own `!` line or it 404s in production while working locally.
- `assets/` and `frames/` are served `immutable, max-age=31536000`. Never
  overwrite a deployed file under the same name: rename it and update the
  reference, or browsers keep the old bytes for a year.
- `index.html` still carries `<meta name="robots" content="noindex">` from when
  this was a review copy. The site is on its final domain now, so that line can
  come off whenever you want the page indexed. Left in deliberately, not by
  oversight.

## The privacy policy is written from the code, so it goes stale

`privacy.html` is not boilerplate. Every claim in it was checked against
`strada-for-agents-fe` and `strada-for-agents-be` on 4 Sep 2026: which
permissions the app really asks for, which vendors really receive data, what is
stored and what is not. **If the app's data handling changes, this page is wrong
until someone re-checks it.** The things most likely to break it: adding
analytics, turning on push (the scaffolding is there but unwired), persisting
voice recordings (today they are transcribed and not stored), or swapping an AI
or infrastructure provider.

## Still open

1. **The legal entity.** "Mithril" appears 4 places: 3 in `privacy.html`
   (marked with an ENTITY NAME comment) and 1 in the `index.html` footer.
   Google Play requires the entity named in the store listing to appear in the
   privacy policy, so keep them matching. Ryan is confirming the exact
   registered name.
2. **The bundle ids in the policy footer describe an app that is not in these
   repos.** `strada-for-agents-fe` is a React + Vite web PWA on Vercel: no Expo,
   no React Native, no iOS or Android project. If a native binary is being built
   somewhere else, the policy should be re-checked against that code, because a
   native shell can request permissions the web app cannot.
3. **No in-app account deletion.** Accounts are created on first eligible
   sign-in, and Apple guideline 5.1.1(v) expects an in-app way to delete one.
   That is an app change, not a site change.
4. **Profile photos and feedback screenshots are served from unlisted but
   public URLs** (`isTypePrivate()` returns false for every upload type). The
   policy says so honestly; making them access controlled would be better.
