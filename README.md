# TUJP Connect Card — deploy to Netlify

This repository contains everything needed to put `connect.theurbanjungleproject.com` live:

- `index.html` — the landing page
- `dries-grasveld.vcf` — the downloadable contact card for the CTA button
- `dries-grasveld.jpg` — the contact photo shown in the contact block
- `jungle-blocks.jpg` — the Jungle Blocks® product photo
- `eu-co-funded.png` — the "Co-funded by the European Union" logo in the footer
- `tujp-logotype.svg` / `tujp-logomark.svg` — the real TUJP logo assets (header wordmark + footer mark)

## Current status

- ✅ HubSpot form is live (portal 26582701)
- ✅ Vimeo video is embedded
- ✅ Jungle Blocks® photo is in place
- ✅ Real TUJP logos are in place
- ✅ Dries's photo is in place in the contact block
- ✅ EU co-funding logo is in the footer

## 1. Deploy to Netlify (free)

1. Go to [app.netlify.com](https://app.netlify.com) and create a (free) account.
2. Choose **"Add new site" → "Deploy manually"**.
3. Drag this whole folder into the upload area. Netlify serves `index.html` automatically as the homepage.
4. You'll get a temporary URL right away, like `https://something-random.netlify.app` — test there first that everything works (form, vCard download, links).

## 2. Connect the real subdomain

1. In Netlify: **Site settings → Domain management → Add a domain** → enter `connect.theurbanjungleproject.com`.
2. Netlify shows a CNAME target (something like `something-random.netlify.app`).
3. Go to the DNS settings for `theurbanjungleproject.com` (with your domain registrar/hosting provider) and add:
   - Type: `CNAME`
   - Name/host: `connect`
   - Value/target: the Netlify address from step 2
4. After DNS propagation (usually within an hour, sometimes up to 24h) Netlify automatically provisions a free SSL certificate — then `https://connect.theurbanjungleproject.com` works.

## 3. Event tracking per channel/trade show

Share the link with a query parameter, e.g.:

```
https://connect.theurbanjungleproject.com/?event=provada26
```

The script in `index.html` automatically passes that value to a hidden HubSpot form field with internal name `event_source`, once that field exists on the form — so in HubSpot you can see which event/channel each lead came from.

## 4. NFC card

Once the page is live, write the final URL (with or without `?event=...`) to the NTAG213 chip in the physical card, using a standard NFC-writer app (e.g. NFC Tools on iOS/Android).
