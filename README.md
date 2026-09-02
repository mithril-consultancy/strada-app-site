# Strada app site

The public home for the **Strada** app (iOS and Android, `com.strada.agents`):
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
- `index.html` carries `<meta name="robots" content="noindex">` so the review
  copy stays out of search. Remove that line (the comment above it marks it)
  once the site is on its final domain.

## Two things to set before store submission

1. **The support email.** `support@stradauae.com` appears 3 times (twice in
   `index.html`, once in `privacy.html`). It is a placeholder until the real
   support address is confirmed. Apple tests the support contact.
2. **The legal entity.** "Mithril" appears 4 places: 3 in `privacy.html`
   (marked with an ENTITY NAME comment) and 1 in the `index.html` footer.
   Google Play requires the entity named in the store listing to appear in
   the privacy policy, so keep them matching.
