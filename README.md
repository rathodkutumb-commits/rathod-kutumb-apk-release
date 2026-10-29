# Rami Mali Rathod Kutumb Shihor — Android App Releases

This repository hosts the official Android app (APK) of **Rami Mali Rathod Kutumb Shihor**:
the family temple, the donation ledger, and the Patotsav / Havan archive, in Gujarati and English.

The app is **not on the Play Store**. Every version is published here as a GitHub release,
and installed apps update themselves from here.

**[⬇ Download the latest APK](https://github.com/rathodkutumb-commits/rathod-kutumb-apk-release/releases/latest/download/rathod-kutumb.apk)**  ·
[All releases](https://github.com/rathodkutumb-commits/rathod-kutumb-apk-release/releases)

---

## Contents

- [For family members: install the app](#for-family-members-install-the-app)
- [How updates reach your phone](#how-updates-reach-your-phone)
- [How this repository works](#how-this-repository-works)
- [Versions and tags](#versions-and-tags)
- [Troubleshooting](#troubleshooting)
- [For maintainers](#for-maintainers)
- [Privacy](#privacy)
- [License](#license)

---

## For family members: install the app

1. On your Android phone, open the **Download the latest APK** link above.
   The file is called `rathod-kutumb.apk`.
2. Open the downloaded file. Android will say the browser (or Files app) isn't allowed to install apps.
   Tap **Settings**, turn on **Allow from this source**, and go back.
3. Tap **Install**, then **Open**.

You only do this once. After that, new versions arrive inside the app.

> Share the download link above, not an APK file forwarded on WhatsApp.
> The link always gives the newest version and the genuine file.

## How updates reach your phone

1. When you open the app, after the splash screen, it quietly checks this repository for a newer release.
2. If one exists, a popup shows **"New update available"**, with the new version number and a short list of what changed.
3. Tap **Update App**. The app downloads the new version with a progress bar and opens Android's installer. Tap **Update**.
   - The first time, Android asks you to allow **"Install unknown apps"** for the Rathod Kutumb app.
     Allow it, come back, and tap **Update App** again.
4. Tap **Later** to skip it for now. The popup comes back the next time you open the app.

Updating keeps all your settings and saved data. If the phone is offline, or there is no new version, the app opens as usual with no popup.

## How this repository works

```
 App source repo (private)                 This repo (public)                    Phones
 ─────────────────────────                 ──────────────────                    ──────
 Developer pushes to main  ──►  GitHub Actions:                   ──►  New release   ──►  App opens, sees a
                                 • runs the tests                       + APK asset         newer version,
                                 • builds a signed release APK                              shows "Update App"
                                 • publishes it here as a release
```

- **No manual steps.** Every push to `main` in the app's source repo starts a GitHub Actions workflow. It runs the tests, builds the APK, signs it with the app's release key, and creates a new release here with the APK attached.
- **This repo holds only releases.** The source code lives in a separate repository, and the repository files never change for a new version. Each release adds just a tag and an APK.
- **Release notes** list the changes made since the previous release.
- **The app reads this repo anonymously.** It asks GitHub's public API for the latest release (`/releases/latest`), compares that version with the one installed, and downloads the attached APK. No login or token is stored in the app.
- **Same signature every time.** Android installs an update only if it is signed with the same key as the installed app. Every release here is signed with the one release key, so updates install over the existing app without losing data.

## Versions and tags

Each release is tagged `v<version>-b<build>`, for example **`v1.1.0-b5`**:

| Part | Meaning |
|---|---|
| `1.1.0` | The version name shown to users. It changes when the developers decide. |
| `b5` | The build number (Android versionCode). It goes up with every release, and the app uses it to decide whether an update is newer. |

Every release has one file attached, `rathod-kutumb.apk`. Because that name never changes,
`releases/latest/download/rathod-kutumb.apk` always points to the newest build.

## Troubleshooting

| Problem | What to do |
|---|---|
| **"App not installed"** when updating | The installed copy was signed with a different key. This happens with an old Play Store copy or a test build. Uninstall the app once, then install from the link above. Future updates will work normally. |
| **The update popup never appears** | Check that the phone is online and reopen the app. If it still doesn't appear, install the latest APK from the link above. |
| **The download stops partway** | Switch to a stronger network and tap **Update App** again. |
| **"Install unknown apps" setting** | Settings → Apps → Rami Mali Rathod Kutumb Shihor → **Install unknown apps** → Allow. |
| **Play Protect warning** | Apps installed outside the Play Store can trigger this. Tap **More details → Install anyway**. Only install from this repository's link. |

## For maintainers

- **Releasing:** push to `main` in the source repo. Pushes that change only documentation (`*.md`, `docs/`) are skipped. To release without a push, run **Actions → Release APK → Run workflow** in the source repo.
- **Required secrets** in the source repo: `RELEASE_REPO_TOKEN` (a fine-grained token with *Contents: read & write* on this repo only), plus the signing secrets `ANDROID_KEYSTORE_BASE64`, `ANDROID_KEYSTORE_PASSWORD`, `ANDROID_KEY_ALIAS`, `ANDROID_KEY_PASSWORD`.
- **The release key must never change.** Keep the keystore and its passwords backed up somewhere safe. If they are lost, every phone has to uninstall and reinstall.
- **Don't delete or re-tag published releases.** Phones that are partway through an update download that release's APK.
- **To roll back a bad release,** fix the problem and push again. The new release gets a higher build number and replaces the bad one on every phone. Publishing an older build won't work, because the app only offers builds newer than the installed one.
- **Full setup guide:** `docs/RELEASES.md` in the source repo.

## Privacy

The update check sends one anonymous request to GitHub's public API when the app opens, plus the APK download when you tap **Update App**.
It sends no personal data, and it uses no tracking or analytics.

## License

Released under the [MIT License](LICENSE).
