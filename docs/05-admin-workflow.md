# 05 — Admin workflow (you as admin)

You are the admin. There is no separate login panel in v1.  
Your “admin panel” is:

1. GitHub **Releases** (upload files)  
2. GitHub **manifest.json** (publish catalog)  

---

## Daily / per game update checklist

When a new BGMI/PUBGM update drops:

1. **Install** that game version on a test device  
2. **Note** exact version name from App info  
3. **Extract / obtain** original `libUE4.so` and `libanogs.so` for that version (authorized)  
4. **Create Release** tag e.g. `bgmi-4.7.0` and upload both `.so` files  
5. **Edit** `manifest.json` — add `versions[]` entry with matching `versionName` and `downloadUrl`s  
6. **Commit** to `main`  
7. On a phone with that game version: open app → setup → **Fetch server** → **Download matching pack**  
8. Run **Live compare** / dump to verify  

---

## Optional: lightweight “admin panel” later

If editing JSON becomes annoying, you can add later:

| Idea | Effort |
|------|--------|
| Google Sheet → export JSON with a script | Low |
| GitHub Actions form (workflow_dispatch inputs) | Medium |
| Small static HTML page that generates JSON for you to paste | Low |
| Firebase console + Cloud Function | Higher |

**Not required for v1.**

---

## App updates (APK)

1. Build new APK  
2. Upload as Release asset e.g. tag `app-v0.27`  
3. Set in manifest:

```json
"appUpdate": {
  "latestVersionCode": 27,
  "latestVersionName": "0.27",
  "apkDownloadUrl": "https://github.com/USER/REPO/releases/download/app-v0.27/app-release.apk",
  "notes": "Bugfixes"
}
```

4. Commit  
Setup screen can show that a newer app version exists.

---

## Security / privacy for admins

- Public repo = public lib links  
- If that is a problem, use a **private** CDN later and protect URLs (not in free GitHub raw easily)  
- Never put Magisk keys or private certificates in the catalog  

---

## Support users when “version not matched”

Tell them:

1. Read installed version from App info  
2. You add that version to the server  
3. Or they paste libs manually into the version folder  

---

## Next

→ [06-connect-app.md](06-connect-app.md)
