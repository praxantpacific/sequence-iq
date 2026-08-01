# SequenceIQ APK (cloud build via GitHub Actions)

This wraps your `index.html` in a minimal Android WebView app. The actual APK
build happens on GitHub's servers — nothing is compiled on your phone.

## Push this from Termux

```bash
pkg install git unzip -y

# unzip this project (adjust path to wherever you downloaded it)
unzip apkproject.zip -d apkproject
cd apkproject

git init
git add -A
git commit -m "Initial commit: WebView wrapper + build workflow"
git branch -M main

# create an empty repo on github.com first, then:
git remote add origin https://github.com/<your-username>/<your-repo>.git
git push -u origin main
```

## Get the APK

1. Go to your repo on GitHub → **Actions** tab. A "Build APK" run starts
   automatically on push (takes ~3-5 min).
2. When it finishes, go to the run → **Releases** (right sidebar of the repo,
   or the repo's main page) → download `app-debug.apk` directly.
   (It's also attached under the workflow run's "Artifacts" section, zipped.)
3. Transfer/open the APK on your phone and tap it to install. You'll need to
   allow "install unknown apps" for your browser/file manager the first time.

## Notes

- This is a **debug** build (unsigned with a debug key) — fine for personal
  installs, not for the Play Store.
- Your page loads Tailwind, Chart.js, Google Fonts, and Font Awesome from
  CDNs, so the app needs internet access at runtime (already enabled via the
  `INTERNET` permission).
- To update the app later: edit `app/src/main/assets/index.html`,
  `git add -A && git commit -m "update" && git push` — a new APK builds
  automatically.
- If you'd rather bundle the CDN assets locally so it works offline, let me
  know and I can help.
