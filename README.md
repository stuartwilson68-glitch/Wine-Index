# Wine Index

A mobile web app to track the bottles of wine in your storage. Add a bottle (with a photo), record where it's stored, and filter your collection by country, region, price and Vivino score.

## What it does

- **Add wines** with: name, country, region, grape, vintage year, price paid, Vivino price, Vivino score, purchase date, storage location and notes.
- **Photo of each bottle** — take one with the camera or pick from your library. It shows next to the wine's details. Photos are resized automatically so they don't fill up your phone.
- **Storage locations** — comes preset with Home, Winedrops and Berry Bros. Add or remove your own (tap the 📍 button).
- **Cellar vs Drunk** — two tabs at the top. The **Cellar** holds the bottles you currently have. When you open one, tap **🍷 Drink!** and it moves to the **Drunk** list, where you record the date, a food pairing, tasting notes and a personal 1–5 star rating. You can edit those notes later, or send a bottle back to the cellar.
- **Filter & sort** by country, region, location, minimum Vivino score, and a min/max price-paid range. Sort by name, vintage, price, market value, Vivino score or your own rating. There's also a search box. Filters apply within whichever tab you're viewing.
- **Number of bottles** — record how many of each wine you hold. The header totals count every bottle, and total paid/market value multiply by quantity. Tapping **🍷 Drink!** on a multi-bottle wine logs one as drunk and leaves the rest in the cellar.
- **Running totals** at the top: number of bottles, total paid, and total market value.
- **Backup & export** (the ⬇ button): save a full backup file (`.json`, includes your photos) to move your collection to another phone or recover it, or export a spreadsheet (`.csv`) to open in Excel/Numbers. You can restore a backup by either merging (adds only wines you don't already have) or replacing everything.
- **"Vivino" button** on every wine opens a Vivino search for that exact wine + vintage, so you can grab the score/price quickly.
- **✨ AI auto-fill (optional):** with an Anthropic API key, snap a bottle label to fill in the name, country, region, grape and year automatically, or import a whole invoice (photo or PDF) to add many wines and prices at once. See "AI auto-fill setup" below.
- **Works offline** and installs to your home screen like a normal app.

All data is stored privately on your own phone (in the browser). Nothing is sent anywhere.

## How to get it on your phone

The app is just a set of files. To use it on your phone it needs to be served over the web (a web address). The easiest free option:

### Option A — GitHub Pages (free, recommended)
1. Create a free account at github.com.
2. Make a new repository, then upload these files into it: `index.html`, `manifest.json`, `sw.js`, `icon-192.png`, `icon-512.png`.
3. In the repo go to **Settings → Pages**, set Source to "Deploy from a branch", branch `main`, folder `/ (root)`, Save.
4. After a minute it gives you a link like `https://yourname.github.io/wine-index/`. Open that on your phone.

### Option B — Netlify Drop (no account, drag & drop)
1. Go to **app.netlify.com/drop** on your computer.
2. Drag the whole folder onto the page. It gives you a live link instantly.

### Install to home screen
Once the app is open on your phone:
- **iPhone (Safari):** tap the Share button → "Add to Home Screen".
- **Android (Chrome):** tap the ⋮ menu → "Install app" / "Add to Home Screen".

It then opens full-screen with its own icon, just like an App Store app.

> You can also just double-click `index.html` to try it on a computer — everything works except camera-on-phone and home-screen install, which need the web-address step above.

## AI auto-fill setup

The label scan and invoice import use Anthropic's Claude vision model. To switch them on:

1. Go to **console.anthropic.com**, add a little credit, and create an API key (Settings → API keys). On the key you can set a monthly spend limit for peace of mind — each label or invoice read costs a fraction of a penny.
2. In the app, tap the **✨** button in the search bar, paste the key, choose a model (Sonnet 4.6 is the recommended balance), and Save.

Then:
- **Bottle label (automatic):** in the Add screen, just take or choose a photo — the app reads the label straight away and fills in the name, country, region, grape and year (blank fields only, so it won't overwrite anything you've typed). The **✨ Auto-fill** button is still there to re-read or override. The detected name is also fed into the **Vivino** search link automatically, so one tap looks it up — no need to re-photograph the bottle.
- **Market price (automatic):** once the name is detected, the app fills the **Market price** field with a rough typical UK price (and shows the low–high range it saw) for quick comparison. It first tries Claude's web search for current shop prices, and if that's unavailable it falls back to a knowledge-based ballpark so you almost always get a figure. Web search is more current — switch it on once in the Anthropic Console under **Settings → Privacy** (about 1p per lookup). The price is only ever a rough guide; adjust it if you know better.
- **Invoice:** tap the **📄** button (above the +), choose an invoice photo or PDF, review the wines it pulls out (edit or untick any), pick a storage location and date, then add them all in one go.

> On Vivino and photos: Vivino's website can't accept an uploaded photo or do reverse-image search through a link (that only works inside Vivino's own app). So the app feeds the AI-detected **name** into Vivino's search for you — you still tap through to read the Vivino score, then type it into the Vivino score field.

**Privacy:** your API key is stored only in this app on your device. Photos/invoices are sent directly from your phone to Anthropic to be read, and nowhere else. The app works fully without a key — AI is entirely optional.

> Note: because the app talks to Anthropic straight from the browser, the key technically lives on your device. That's fine for personal use; just keep the spend limit on and don't share the key.

## Notes & next steps

- **Vivino:** Vivino has no public API, so the Vivino score is a field you fill in (the Vivino button makes the lookup quick).
- **Invoice import & auto-reading bottle photos:** now built in — see "AI auto-fill setup" above. Optional; needs an Anthropic API key.
- **Backup:** because data lives in your browser, avoid "clear website data" for this site. Use the ⬇ Backup button to export a `.json` file regularly — that's your safety net and the way to move everything to a new phone.
