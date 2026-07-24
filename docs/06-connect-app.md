# 06 — Connect the Android app to your server

## After the catalog works in the browser

Raw URL example:

```text
https://raw.githubusercontent.com/YOUR_USER/ue4dumper-catalog/main/manifest.json
```

---

## A) Temporary: paste URL in the app (no rebuild)

1. Install APK  
2. Accept **Agreement**  
3. On **Environment setup**:
   - Paste the raw URL into **Catalog manifest URL**  
   - Tap **Fetch server**  
4. For each game card:
   - Check **Installed version**  
   - If match: **Download matching pack**  
5. **Finish setup**  

If fetch fails:

- URL wrong / private repo  
- No internet  
- Invalid JSON  

Status line on the setup screen shows the error.

---

## B) Permanent: hardcode default URL (rebuild APK)

Edit:

```text
android-app/app/src/main/java/com/ue4dumper/app/prefs/AppPrefs.kt
```

Change:

```kotlin
const val DEFAULT_MANIFEST_URL =
    "https://raw.githubusercontent.com/YOUR_USER/ue4dumper-catalog/main/manifest.json"
```

Rebuild:

```bat
cd android-app
set JAVA_HOME=C:\Program Files\Java\jdk-17
gradlew.bat :app:assembleDebug
```

---

## Where downloads go on the device

```text
/sdcard/UE4Dumper/reference/<gameId>/<versionName>/libUE4.so
/sdcard/UE4Dumper/reference/<gameId>/<versionName>/libanogs.so
```

Example:

```text
/sdcard/UE4Dumper/reference/bgmi/4.4.0/libUE4.so
```

Runtime **Dump only** still uses:

```text
/sdcard/UE4Dumper/runtime/
```

---

## Manual setup without server

1. Create folders yourself (use `game id` + `versionName` from manifest)  
2. Copy `.so` files in  
3. **Skip for now** on setup (or Finish)  
4. Use Runtime / Hex with those files  

Server remains **recommended**.

---

## Test plan

| Test | Expected |
|------|----------|
| Open raw manifest in browser | JSON visible |
| Fetch server in app | Games listed |
| Game installed, version in catalog | “Matched…” + Download enabled |
| Game installed, version missing | Message lists available versions |
| Download pack | Files appear under `reference/...` |
| No network after first fetch | Cached catalog may still load |
| Bad URL | Clear error on status line |

---

## Troubleshooting

| Problem | Fix |
|---------|-----|
| HTTP 404 on fetch | Wrong raw path / branch not `main` |
| Download fails HTTP 404 | Wrong release tag or filename |
| Download fails but browser works | Try again; app also tries root curl/wget |
| Version never matches | Align `versionName` with App info exactly |
| Empty game list | Empty `games` array or parse error — validate JSON |

---

## You are done when

- [ ] Manifest URL works in browser  
- [ ] App Fetch server shows BGMI / PUBGM  
- [ ] Download pack fills `reference/` folders  
- [ ] Installed version matches a pack on your test phone  

Then use **Runtime** (dump / live compare / inject compare) and **Hex** as before.
