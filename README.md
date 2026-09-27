# 5 o'clock somewhere

A single-file drinks-discovery app themed around "it's 5 o'clock somewhere." At any moment it finds the country (or countries) currently striking 5:00pm local time and shows a signature drink for that place, with a hand-drawn geographic silhouette, ingredients, and a recipe.

## Files

| File | Purpose |
|---|---|
| `index.html` / `five-pm-somewhere.html` / `five-oclock-somewhere.html` | The complete app (identical copies — `index.html` is what a static host will serve by default) |
| `manifest.json` | PWA manifest, referenced by the app's `<head>` once hosted |
| `assetlinks.json` (also under `.well-known/`) | Android TWA domain-verification file — still has placeholder package name + signing fingerprint, see checklist |
| `icon-192.png`, `icon-512.png`, `icon-maskable-512.png` | App icons referenced by `manifest.json` |
| `PLAY-STORE-CHECKLIST.md` | Full remaining steps to publish on Google Play |

## Status

App logic, content, age/legal gate, Terms/Privacy, and the 199-country dataset are complete. What's left is entirely deployment/publishing work — see `PLAY-STORE-CHECKLIST.md` for the itemized list (hosting, Play Console account, TWA packaging, signing fingerprint, store listing).

## Hosting

Once this repo is public (or Pages is enabled), GitHub Pages can serve `index.html` directly at `https://<username>.github.io/5pm-app-claude/` — that single step knocks out checklist items 1–2 (real HTTPS domain + manifest link target).
