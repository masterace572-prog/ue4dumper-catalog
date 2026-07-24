# 03 — `manifest.json` schema (exact format)

The app downloads this file and parses it with `CatalogParser`.  
If a field is wrong or missing, fetch/download can fail.

---

## Full structure

```json
{
  "schemaVersion": 1,
  "appMinVersionCode": 26,
  "appUpdate": {
    "latestVersionCode": 26,
    "latestVersionName": "0.26",
    "apkDownloadUrl": "https://github.com/USER/REPO/releases/download/app-v0.26/app-release.apk",
    "notes": "Optional update message"
  },
  "games": [
    {
      "id": "bgmi",
      "displayName": "BGMI",
      "packageName": "com.pubg.imobile",
      "versions": [
        {
          "versionName": "4.4.0",
          "versionCode": 0,
          "notes": "Optional note for this pack",
          "libs": [
            {
              "id": "ue4",
              "fileName": "libUE4.so",
              "label": "libUE4.so (BGMI 4.4.0)",
              "downloadUrl": "https://github.com/USER/REPO/releases/download/bgmi-4.4.0/libUE4.so",
              "sha256": "",
              "sizeBytes": 0
            }
          ]
        }
      ]
    }
  ]
}
```

---

## Field reference

### Root

| Field | Required | Meaning |
|-------|----------|---------|
| `schemaVersion` | yes | Use `1` for now |
| `appMinVersionCode` | no | Soft hint: minimum app build that understands this catalog |
| `appUpdate` | no | Tell the app a newer APK exists |
| `games` | yes | Array of games |

### `appUpdate` (optional)

| Field | Required | Meaning |
|-------|----------|---------|
| `latestVersionCode` | yes | Integer, compare to app `versionCode` |
| `latestVersionName` | yes | e.g. `"0.27"` |
| `apkDownloadUrl` | no | Direct APK link (Release asset) |
| `notes` | no | Changelog text |

### Each game

| Field | Required | Meaning |
|-------|----------|---------|
| `id` | yes | Short id folder name: `bgmi`, `pubgm` (no spaces) |
| `displayName` | yes | Shown in UI: `BGMI` |
| `packageName` | yes | Android package: `com.pubg.imobile` |
| `versions` | yes | List of packs |

### Each version

| Field | Required | Meaning |
|-------|----------|---------|
| `versionName` | yes | Must match installed app version string when possible |
| `versionCode` | no | `0` = ignore; else match Android versionCode |
| `notes` | no | Admin note |
| `libs` | yes | Files to download for this pack |

### Each lib

| Field | Required | Meaning |
|-------|----------|---------|
| `id` | yes | Short key: `ue4`, `anogs` |
| `fileName` | yes | Saved as this name, e.g. `libUE4.so` |
| `label` | no | Friendly name in logs |
| `downloadUrl` | yes | **Direct** HTTPS URL to the file |
| `sha256` | no | Optional integrity check (hex) |
| `sizeBytes` | no | Optional; used for progress if server omits size |

---

## How the app matches installed game → pack

1. Read installed `versionName` / `versionCode` from the package  
2. Prefer **exact** `versionName` match (case-insensitive, ignore leading `v`)  
3. Else try `versionCode` if both > 0  
4. Else show error: installed version has **no pack** — list available versions  

So if the phone has BGMI `3.9.0`, you need a `"versionName": "3.9.0"` entry (or correct versionCode).

---

## Where files land on the phone after download

```text
/sdcard/UE4Dumper/reference/<gameId>/<versionName>/<fileName>
```

Example:

```text
/sdcard/UE4Dumper/reference/bgmi/4.4.0/libUE4.so
/sdcard/UE4Dumper/reference/bgmi/4.4.0/libanogs.so
```

---

## URL rules

| Good | Bad |
|------|-----|
| `.../releases/download/tag/libUE4.so` | `.../releases/tag/bgmi-4.4.0` (HTML page) |
| `https://...` | Missing `https://` |
| Raw CDN link | Link that needs login |

---

## Validate JSON before commit

- Use https://jsonlint.com  
- Or VS Code — red squiggles on invalid JSON  
- One trailing comma breaks the whole catalog  

---

## Next

→ [04-add-game-and-version.md](04-add-game-and-version.md)
