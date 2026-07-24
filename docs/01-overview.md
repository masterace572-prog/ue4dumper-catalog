# 01 — Overview: how the “server” works

## Big picture

```
┌──────────────────┐         1. GET manifest.json          ┌─────────────────────┐
│  UE4Dumper app   │ ───────────────────────────────────► │  GitHub (raw file)   │
│                  │                                       │  list of games/libs  │
│  Setup screen    │                                       └─────────────────────┘
│                  │
│                  │         2. GET lib files (in-app)     ┌─────────────────────┐
│  Download pack   │ ───────────────────────────────────► │  GitHub Releases     │
│                  │                                       │  .so assets          │
└──────────────────┘                                       └─────────────────────┘
         │
         ▼
  /sdcard/UE4Dumper/reference/<gameId>/<version>/libUE4.so
```

There is **no custom backend code** in this setup.  
GitHub hosts:

1. **Catalog** = small JSON file (`manifest.json`)
2. **Files** = Release attachments (libs)

The app:

1. Reads installed game version (e.g. BGMI `4.4.0`)
2. Finds a matching entry in `manifest.json`
3. Downloads those libs into the phone folder
4. Uses them for **live compare / dump** later

---

## What lives where

| Data | Location | Who updates |
|------|----------|-------------|
| Game list (BGMI, PUBGM, …) | `manifest.json` → `games[]` | You (admin) |
| Version list (4.4.0, 4.5.0, …) | `manifest.json` → `versions[]` | You |
| Download URLs | `manifest.json` → `libs[].downloadUrl` | You |
| Actual `.so` bytes | GitHub **Release** assets | You |
| Which pack is on phone | Device folders | App after download |

---

## App flow for the user

1. **Agreement** (first launch)
2. **Environment setup**
   - Enter catalog URL (or default)
   - Fetch server
   - See installed game version
   - Download matching pack **or** paste files manually
3. **Main app** (UE4Dumper / Runtime / Hex)

---

## Safety

- App only **reads** game process memory (with root) and **writes** under `/sdcard/UE4Dumper` (+ small temp under `/data/local/tmp`).
- Server is **HTTPS download only** — no push from phone to your server required for v1.
- Hosting public libs = public links. Do not upload private secrets.

---

## Next

→ [02-github-setup-step-by-step.md](02-github-setup-step-by-step.md)
