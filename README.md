# UE4Dumper catalog server — how to implement

This folder is your **server side** for the Android app.

You do **not** need a paid VPS for the first version.  
Use **GitHub** as the server:

| Need | GitHub feature |
|------|----------------|
| List of games + versions + download links | `manifest.json` file in a repo |
| Large files (`libUE4.so`, `libanogs.so`) | **Releases** (file attachments) |
| App APK updates (optional) | Also a Release asset |

---

## Read these files in order

| # | File | What it teaches |
|---|------|-----------------|
| 1 | [01-overview.md](01-overview.md) | How the app talks to the server |
| 2 | [02-github-setup-step-by-step.md](02-github-setup-step-by-step.md) | Create repo, first release, first manifest |
| 3 | [03-manifest-schema.md](03-manifest-schema.md) | Exact JSON fields the app understands |
| 4 | [04-add-game-and-version.md](04-add-game-and-version.md) | Add BGMI/PUBG versions & libs online |
| 5 | [05-admin-workflow.md](05-admin-workflow.md) | Daily admin: push libs, match game versions |
| 6 | [06-connect-app.md](06-connect-app.md) | Point the APK at your catalog URL |

Also:

- `manifest.json` — ready template (replace `YOUR_USER`)
- `../SERVER_PLAN.md` — architecture summary

---

## Quick start (5 minutes)

1. Create GitHub repo: `ue4dumper-catalog` (public).
2. Upload `manifest.json` to the `main` branch.
3. Create a Release (example tag `bgmi-4.4.0`) and upload `libUE4.so` + `libanogs.so`.
4. Put the real download links into `manifest.json` and commit.
5. In the app **Environment setup** screen, paste:

```text
https://raw.githubusercontent.com/YOUR_USER/ue4dumper-catalog/main/manifest.json
```

6. Tap **Fetch server** → **Download matching pack**.

Done. The app downloads **inside the app** (not a browser).
