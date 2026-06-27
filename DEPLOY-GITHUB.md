# Deploying Wine Index on GitHub Pages

The app is plain files, so "deploying" just means putting them in a GitHub repository with **Pages** turned on. Updating later means uploading the changed files again — GitHub rebuilds the site automatically.

The files that make up the app:
`index.html`, `manifest.json`, `sw.js`, `icon-192.png`, `icon-512.png`
(The `.md` guides are optional — they don't affect the app.)

---

## First time only — create the site

1. Go to **github.com**, sign in (or create a free account).
2. Click **+** (top right) → **New repository**. Name it e.g. `wine-index`, set it **Public**, click **Create repository**.
3. On the new repo page click **uploading an existing file** (or **Add file → Upload files**).
4. Drag in the five app files listed above. Scroll down and click **Commit changes**.
5. Go to **Settings → Pages**. Under **Build and deployment**, set **Source = Deploy from a branch**, **Branch = main**, folder **/ (root)**, click **Save**.
6. Wait ~1 minute, then refresh. Pages shows your live link, like:
   `https://YOURNAME.github.io/wine-index/`
   Open that on your phone and **Add to Home Screen**.

---

## Deploying an update (what you want now)

1. Open your repo on github.com.
2. Click into the file you changed — for this update that's **`index.html`** and **`sw.js`** (and the `.md` files if you want the latest copies).
3. Click the **pencil ✏️ (Edit)** icon → delete the contents → paste the new contents from this folder → **Commit changes**.

   *Easier for several files:* on the repo home click **Add file → Upload files**, drag the updated files in (uploading a file with the same name overwrites it), then **Commit changes**.
4. GitHub Pages redeploys automatically in about a minute. Your link stays the same.

### Seeing the update on your phone
- In a browser: just reload the page.
- Installed to the home screen: open it **with internet** and it now pulls the latest page automatically (the service worker was set to network-first for exactly this). If you ever see a stale screen, close and reopen the app, or pull-to-refresh.

> Tip: each time the app's cached files change, `sw.js` has a `CACHE` version near the top (currently `wine-index-v2`). If you make your own edits later and want to force every device to refresh, bump it to `v3`, etc. For updates I hand you, I'll bump it when needed.

---

## Git option (if you prefer the command line)

If you have Git installed and cloned the repo:

```
git add .
git commit -m "Update Wine Index"
git push
```

Pages redeploys on push. The web-upload method above does exactly the same thing without needing Git.

---

## Note on the Android APK

If you built the APK with PWABuilder pointing at your GitHub Pages link, you usually **don't** need to rebuild it — it loads your live site, so it picks up deployed updates on its own. Only rebuild if you change the app icon, name, or package settings (see BUILD-ANDROID-APK.md).
