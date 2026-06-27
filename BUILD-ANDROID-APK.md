# Build a real Android app (.apk) for Wine Index

This turns Wine Index into an actual installable Android app file. It takes about 15 minutes and is free. There are two stages:

1. **Put the app online** (so it has a web address) — 5 min.
2. **Generate the `.apk` with PWABuilder** and install it on your phone — 10 min.

You don't need to be a developer. Just follow the steps in order.

---

## Stage 1 — Put the app online (free, no account)

PWABuilder needs a live web link to your app. The easiest way is **Netlify Drop**.

1. On a computer, open **https://app.netlify.com/drop** in your browser.
2. Open the **Wine Index App** folder on your computer (the one containing `index.html`, `manifest.json`, `sw.js`, `icon-192.png`, `icon-512.png`).
3. Drag that whole folder onto the Netlify Drop page.
4. After a few seconds it shows a live link like `https://wonderful-wine-123.netlify.app`. **Copy it.**
5. Open the link once in your browser to check the app loads. 

> Want a tidier name or to keep it long-term? Create a free Netlify account when prompted — the same link stays live. (A free GitHub Pages site also works if you prefer.)

Keep this URL handy — you'll paste it into PWABuilder next, and you'll also use it when you want to update the app later.

---

## Stage 2 — Generate the .apk with PWABuilder

PWABuilder is Google/Microsoft's free tool that wraps a web app into an Android package and signs it for you.

1. On the computer, open **https://www.pwabuilder.com**.
2. Paste your Netlify link into the box and click **Start** / **Analyze**. It will check the app and show a score (the manifest and icons are already set up, so it should pass).
3. Click **Package For Stores**, then find the **Android** card and click **Generate Package**.
4. In the Android options:
   - Leave **Package ID** as suggested, or set something like `com.yourname.wineindex` (lowercase, no spaces — this is permanent for the app's identity).
   - **App name:** Wine Index.
   - Leave **Signing key** on **"Create new"** (PWABuilder makes and signs with a fresh key for you).
5. Click **Download**. You get a **zip file**.

### What's in the zip
- **`*.apk`** — this is the file you install on your phone (sideloading / testing). ← the one you want.
- `*.aab` — only needed if you ever publish to the Google Play Store.
- **`signing.keystore`** and **`signing-key-info.txt`** — your signing key and its passwords. **Keep these safe and private** — you need the *same* key to release any future update of the app.

Unzip the file and locate the `.apk`.

---

## Stage 3 — Install the .apk on your Android phone

1. Get the `.apk` onto your phone — email it to yourself, put it in Google Drive, or copy via USB, then open it in your phone's **Files** app.
2. Tap the `.apk`. Android will warn that it's from an unknown source. Tap **Settings** → enable **"Allow from this source"** for the app you're installing from (Files/Chrome), then go back and tap **Install**.
3. Open **Wine Index** from your app drawer. It runs full-screen with its own icon, like any other app. 

That's it — you now have a real Android app.

---

## Optional polish — remove the small address bar

Because the app is a "Trusted Web Activity", Android may briefly show a thin web address bar at the top on first launch. To remove it permanently (optional, only matters cosmetically):

1. In the PWABuilder zip there's an **`assetlinks.json`** file (and PWABuilder shows the same content under "Next steps").
2. Put that file online at your site so it's reachable at:
   `https://your-netlify-link/.well-known/assetlinks.json`
   With Netlify Drop: add a folder named `.well-known` containing `assetlinks.json` into the Wine Index App folder, then re-drag the folder to Netlify (re-deploy).
3. Reopen the app — the bar disappears.

You can skip this entirely for personal use; the app works fine either way.

---

## Updating the app later

When I change the app, you:
1. Re-drag the updated folder to Netlify (the link stays the same).
2. Because it's a Trusted Web Activity, the installed app loads the latest version automatically the next time it's online — usually **no need to rebuild the APK** for content changes.
3. Only rebuild via PWABuilder if you change the app's name, icon, or package settings — and when you do, choose **"Use existing key"** and upload the `signing.keystore` from before, so the update installs over the old app.

---

## Important notes

- **Internet:** a Trusted Web Activity app loads your hosted site, and the built-in offline cache keeps it working without signal after the first open. So keep the Netlify link live — if you delete it, the app stops loading.
- **Prefer a fully offline, self-contained app with no hosting?** That's also possible but needs Android Studio on a computer to build (a bigger setup). Tell me and I'll generate a ready-to-build project for that route instead.
- **Your data** stays on the phone (in the app's storage). Use the in-app **⬇ Backup** button now and then to export a `.json` you can keep safe.
