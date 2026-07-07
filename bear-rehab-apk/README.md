# 🐻 Bear Rehab — offline field APK (never-online)

A fully **offline** Android app for CCA's sun-bear cub care at Boronipara.
It runs with **zero internet**, logs feeding / walking / health / weight, shows the
protocols, and **exports a file** you Bluetooth to another phone. No sign-in, no server.

The `.apk` is built automatically in **GitHub's cloud** — nobody needs Android Studio.

---

## How to get the APK (one-time, ~5 minutes)

1. Create a new repository on **github.com** (e.g. `bear-rehab-apk`). Private is fine.
2. Upload **everything in this folder** to that repo:
   - On github.com: *Add file → Upload files* → drag the whole folder's contents → Commit.
   - Or with git:
     ```
     cd bear-rehab-apk
     git init && git add . && git commit -m "Bear Rehab offline app"
     git branch -M main
     git remote add origin https://github.com/<you>/bear-rehab-apk.git
     git push -u origin main
     ```
3. GitHub Actions starts **automatically**. Open the **Actions** tab and wait ~5–8 min for the ✅.
4. Download the APK:
   - From the **Releases** page (right sidebar) → `BearRehab.apk`, **or**
   - From the finished Actions run → **Artifacts → BearRehab-APK**.
5. Send `BearRehab.apk` to Caesar / the Hub to host, and/or Bluetooth it straight to phones.

To rebuild after any change: just push again, or click **Run workflow** in the Actions tab.

---

## Installing on phones (offline)

- Transfer `BearRehab.apk` to a phone by **Bluetooth / Quick Share / cable** — no internet needed.
- Tap the file → allow **"Install from unknown sources"** → Install.
- Open it — it works fully offline, forever.

## Getting the data out (offline handoff)

1. On the field phone: **🔄 শেয়ার → 📤 ডেটা পাঠান** → sends a `bear-data-*.json` file.
2. Bluetooth that file to the phone that travels to town.
3. In town, open the **Hub app** (online) → **🔄 শেয়ার → 📥 ডেটা নিন** → pick the file → it uploads.
   (The file format matches the Hub's importer, and duplicates are ignored.)

---

## What's inside

| File | Purpose |
|---|---|
| `www/index.html` | the entire offline app (self-contained) |
| `www/baloo.png` | header logo |
| `resources/icon.png` | app icon (Baloo) — auto-resized at build |
| `capacitor.config.json` | app id `org.conservationalliance.bearrehab`, name "Bear Rehab" |
| `package.json` | Capacitor dependencies |
| `.github/workflows/build-apk.yml` | the cloud build (JDK 17 + Android SDK + Gradle) |

The APK is **debug-signed** — perfectly installable by sideloading. (For Play Store you'd
add a release keystore, but that's not needed for field distribution.)

## Notes / limits
- Built and shipped without a device test — if anything misbehaves on a real phone, send a
  screenshot and it's a quick fix + re-push.
- This offline app is a **collector**: it does not talk to the server at all. The live maps,
  reports and auto-weather stay in the online Hub app; this one just captures + exports.
