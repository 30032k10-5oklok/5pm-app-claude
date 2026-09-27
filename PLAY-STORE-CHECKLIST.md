# "5 o'clock somewhere" — Google Play readiness checklist

## Already done in the app

- **Paywall removed.** No subscription gate, unlock codes, or locked content remain — every country and feature is open.
- **Age/legal gate on first launch.** A `#gate` screen requires checking "I'm of legal drinking age" and "I agree to the Terms" before the app is usable. Choice is remembered via `localStorage` (`fiveoclock.terms_ok_v1`).
- **Terms of Service and Privacy Policy screens**, each reachable from the gate and from in-app links, with real section content (not placeholders), except for a few fields only you can fill in (see below).
- **PWA meta tags**: description, light/dark `theme-color`, and a commented-out `<link rel="manifest">` / apple-touch-icon pointing at the packaging files below.
- **`manifest.json`, `assetlinks.json`, and three icons** (`icon-192.png`, `icon-512.png`, `icon-maskable-512.png`) generated and matched to the app's own color palette — these are templates ready for you to finish (see below).
- **Ingredient links**: every ingredient, including alcoholic ones, links to Amazon search/affiliate results, per your instruction. See the alcohol-policy note below — this is a real risk to be aware of, left as-is deliberately.

## Things only you can do

1. **Host the file somewhere with a real HTTPS domain.**
   Play Store apps built as a Trusted Web Activity (TWA) need a live URL, not just a local file. Any static host works (GitHub Pages, Netlify, Cloudflare Pages, your own server). Upload `five-pm-somewhere.html` (renamed to `index.html` or referenced directly), plus `manifest.json` and the three icon PNGs, all in the same folder.

2. **Uncomment the manifest link in the HTML `<head>`**
   Once hosted, uncomment:
   ```html
   <link rel="manifest" href="manifest.json">
   <link rel="apple-touch-icon" href="icon-192.png">
   ```

3. **Fill in the Privacy Policy placeholders** inside the HTML's `PRIVACY` object:
   - `controller`: your name or registered business name
   - `host`: whoever hosts the file (e.g. "Netlify")
   Your email is already filled in. Also check whether you need to pay the UK ICO's data protection fee (ico.org.uk) if you're UK-based.

4. **Create a Google Play Console developer account** ($25 one-time fee) at play.google.com/console if you don't have one.

5. **Package the site as an Android app (TWA)** using either:
   - **[PWABuilder](https://www.pwabuilder.com/)** — paste your hosted URL, it detects the manifest, and generates a signed Android App Bundle (.aab) for you. Easiest path.
   - **[Bubblewrap CLI](https://github.com/GoogleChromeLabs/bubblewrap)** — more control, requires Node.js locally.
   Either tool will generate (or ask you to generate) a signing key, and will need your app's package name (e.g. `com.yourname.fiveoclocksomewhere`).

6. **Finish `assetlinks.json`** with the real values from step 5:
   - Replace `com.example.fiveoclocksomewhere` with your actual package name.
   - Replace `REPLACE_WITH_YOUR_APP_SIGNING_SHA256_FINGERPRINT` with your app's real SHA-256 signing certificate fingerprint (PWABuilder/Bubblewrap will show you this, or get it from Play Console after upload).
   - Host this file at `https://yourdomain.com/.well-known/assetlinks.json` — this is what proves to Android that your app and your website are the same thing (so the TWA opens without a browser address bar).

7. **Upload the .aab to Play Console**, then complete:
   - **Content rating questionnaire** — flag alcohol references/depiction honestly; this typically pushes the rating to teen/mature rather than "everyone," which is expected and fine, but must be answered accurately.
   - **Data Safety form** — since the app only uses `localStorage` and makes no network calls to your own servers (Amazon links are just outbound links, not data collection), you can generally declare "no data collected."
   - **Store listing**: title, short description, full description, screenshots, feature graphic. I can help draft this copy if you want it.

8. **⚠️ Alcohol content policy risk (flagged, not resolved in code, per your instruction).**
   Google Play's policy on alcohol restricts apps that "facilitate the sale of alcohol" or target it inappropriately. Your ingredient list links every ingredient — including spirits, wine, and beer — directly to Amazon search results. I built and then removed an alcohol-detection filter that would have suppressed just those links; you told me to leave all alcohol links in, and I have. Be aware this is the single most likely reason Play could reject the app or require additional review (e.g., confirming it doesn't function as an alcohol storefront, or requiring more visible responsible-drinking messaging). If it's rejected on this basis, the fix would be to remove/replace just the alcohol-ingredient Amazon links — I can re-add that suppression instantly if you change your mind later; the code for it is simple to reintroduce.

## Files in this delivery

| File | Purpose |
|---|---|
| `five-pm-somewhere.html` | The complete app (also matches the published Claude artifact) |
| `manifest.json` | PWA manifest — needs hosting alongside the HTML file |
| `assetlinks.json` | TWA domain-verification template — needs your real package name + signing fingerprint |
| `icon-192.png`, `icon-512.png`, `icon-maskable-512.png` | App icons, referenced by `manifest.json` |
