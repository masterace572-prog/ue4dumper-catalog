# 04 — Add a game or a new version online

No APK rebuild. Only GitHub + `manifest.json`.

---

## A) Add a **new game** (example: PUBG KR)

### 1. Upload libs to a Release

- Tag: `pubgkr-1.0.0`  
- Files: `libUE4.so`, `libanogs.so` (or whatever you support)

### 2. Append a game object in `manifest.json`

```json
{
  "id": "pubg_kr",
  "displayName": "PUBG KR",
  "packageName": "com.pubg.krmobile",
  "versions": [
    {
      "versionName": "1.0.0",
      "versionCode": 0,
      "libs": [
        {
          "id": "ue4",
          "fileName": "libUE4.so",
          "label": "libUE4.so (KR)",
          "downloadUrl": "https://github.com/YOUR_USER/ue4dumper-catalog/releases/download/pubgkr-1.0.0/libUE4.so",
          "sizeBytes": 0
        }
      ]
    }
  ]
}
```

### 3. Commit to `main`

### 4. In the app

**Fetch server** again → new game appears on setup list.

---

## B) Add a **new version** for an existing game (example: BGMI 4.6.0)

### 1. Get the real version string from a phone

Settings → Apps → BGMI → **Version**  
Example: `3.9.0` or `4.6.0`  

Use **that exact string** as `versionName`.

### 2. Create Release

- Tag: `bgmi-4.6.0`  
- Upload the libs that belong to **that** build  

### 3. Add under `games[bgmi].versions`

```json
{
  "versionName": "4.6.0",
  "versionCode": 0,
  "notes": "BGMI 4.6.0 reference",
  "libs": [
    {
      "id": "ue4",
      "fileName": "libUE4.so",
      "label": "libUE4.so (BGMI 4.6.0)",
      "downloadUrl": "https://github.com/YOUR_USER/ue4dumper-catalog/releases/download/bgmi-4.6.0/libUE4.so",
      "sizeBytes": 0
    },
    {
      "id": "anogs",
      "fileName": "libanogs.so",
      "label": "libanogs.so (BGMI 4.6.0)",
      "downloadUrl": "https://github.com/YOUR_USER/ue4dumper-catalog/releases/download/bgmi-4.6.0/libanogs.so",
      "sizeBytes": 0
    }
  ]
}
```

### 4. Commit

Users with BGMI 4.6.0 will see **matched** and can download.

Users on 4.5.0 keep using the 4.5.0 pack.

---

## C) Update libs for an **existing** version

Two options:

### Option 1 — Replace assets on same tag (careful)

GitHub Releases can edit and re-upload the same filename.  
Old URLs stay the same; app re-download gets new file.

### Option 2 — New tag (safer)

- Tag `bgmi-4.6.0-r2`  
- Update `downloadUrl` in manifest  
- Commit  

Users tap **Re-download pack**.

---

## D) Manual path (if user has no network)

User copies files into:

```text
/sdcard/UE4Dumper/reference/bgmi/4.6.0/libUE4.so
/sdcard/UE4Dumper/reference/bgmi/4.6.0/libanogs.so
```

(`bgmi` = `id` from manifest, `4.6.0` = `versionName`)

Server setup is still **recommended**.

---

## Common mistakes

| Mistake | Result |
|---------|--------|
| `versionName` is `4.6` but game shows `4.6.0` | No match |
| HTML release page as `downloadUrl` | Download fails |
| Forgot to commit manifest after release | App still shows old list |
| Private repo without token | App cannot fetch raw JSON |

---

## Next

→ [05-admin-workflow.md](05-admin-workflow.md)
