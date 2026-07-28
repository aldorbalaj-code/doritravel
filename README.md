# Dori Travel — Formulari Digjital

## Deploy (Vercel — 5 minutes)

1. Krijo një repo të ri në GitHub dhe ngarko gjithë këtë folder (`api/`, `public/`, `package.json`, `vercel.json`).
2. Shko te https://vercel.com → **Add New Project** → zgjidh repon.
3. Vercel do ta identifikojë automatikisht si projekt statik + serverless functions. Mos ndrysho asgjë në "Build Settings".
4. Para se të bësh Deploy, shto Environment Variable:
   - **Key:** `ANTHROPIC_API_KEY`
   - **Value:** çelësi yt nga https://console.anthropic.com/settings/keys
5. Kliko **Deploy**. Do të marrësh një link (p.sh. `dori-travel.vercel.app`) — ky është linku që hapet nga telefoni.

## Local testing

```
npm i -g vercel
vercel dev
```

Then open http://localhost:3000 — this runs both the static frontend and the `/api/extract` function together, same as production.

## Notes

- The Anthropic API key lives only in `api/extract.js`, read from the server-side environment variable. It is never sent to the browser.
- `Shkarko PDF` is enabled as soon as at least one photo/row has been added — regardless of how many of the 20 slots are filled or whether AI extraction succeeded for every row.
- If a card photo fails to extract, the row stays blank/editable rather than blocking anything — fill it in by hand.
