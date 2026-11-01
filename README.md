# Cosy Castle — iOS app

Thin native wrapper (Capacitor) that loads the live web app **https://cosy-castle.netlify.app**.
Same approach as the Instal Habitat app: a web update is instantly live in the iOS app too.

- **App name:** Cosy Castle
- **Bundle ID:** `com.cosycastle.app`
- **Loads:** https://cosy-castle.netlify.app
- **Apple account:** your existing Apple Developer account (no extra payment to add an app)

---

## Option A — You have a Mac with Xcode (fastest)

```bash
npm install
npx cap add ios
npx capacitor-assets generate --ios     # builds the icon + splash from /resources
npx cap sync ios
npx cap open ios                         # opens Xcode
```

In Xcode:
1. Select the **App** target → **Signing & Capabilities** → your Team, Bundle ID `com.cosycastle.app`.
2. **Product → Archive** → **Distribute App → App Store Connect → Upload**.
3. In App Store Connect: create the app record (`com.cosycastle.app`), then it shows up in **TestFlight**.

### Reuse the Instal Habitat Xcode project (even faster)
If you already have the Instal Habitat Capacitor/Xcode project, just duplicate it and change three things:
- **Bundle Identifier** → `com.cosycastle.app`
- **Display name** → Cosy Castle
- the loaded URL (in `capacitor.config.json`, `server.url`) → `https://cosy-castle.netlify.app`
Then swap the app icon for the Cosy Castle one and re-archive.

---

## Option B — No Mac (build in the cloud, from Windows)

Use **Codemagic** (`codemagic.yaml` is included):
1. Push this folder to a GitHub repo (e.g. `CosyCastle/cosy-castle-ios`).
2. Create a free Codemagic account, add the repo.
3. In Codemagic → Teams → **Integrations**: connect **App Store Connect** (API key from your Apple account).
4. Set the signing bundle id to `com.cosycastle.app`.
5. Run the **Cosy Castle iOS** workflow → it builds on a cloud Mac and pushes straight to **TestFlight**.

---

## App Store Connect (both options)
1. App Store Connect → **Apps → +** → New App.
2. Platform iOS · Name **Cosy Castle** · Bundle ID `com.cosycastle.app` · SKU `cosycastle`.
3. Under **TestFlight**, add testers (same as you did for Instal Habitat).

## Note on review
Apple guideline 4.2 can flag "website-only" apps. Instal Habitat passed with the same wrapper,
so keep the native shell (splash screen, offline fallback) — it's already set up here.
