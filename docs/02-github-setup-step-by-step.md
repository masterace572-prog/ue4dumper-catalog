# 02 — GitHub setup (step by step)

Follow this exactly the first time.

---

## Step 1 — Create the catalog repository

1. Open https://github.com/new  
2. **Repository name:** `ue4dumper-catalog` (or any name)  
3. Visibility: **Public** (simplest for raw URLs + Releases downloads)  
4. Check **Add a README**  
5. Create repository  

Your repo will look like:

```text
https://github.com/YOUR_USER/ue4dumper-catalog
```

Replace `YOUR_USER` with your GitHub username everywhere below.

---

## Step 2 — Add `manifest.json`

1. In the repo click **Add file → Upload files** (or Create new file)  
2. Upload the file from this project:

```text
ue4dumper/server-catalog/manifest.json
```

3. Open it on GitHub and edit:
   - Replace every `YOUR_USER` with your username  
4. Commit to **main** branch  

After commit, the raw URL is:

```text
https://raw.githubusercontent.com/YOUR_USER/ue4dumper-catalog/main/manifest.json
```

Open this URL in a browser — you should see the JSON text.  
**If it 404s, the app cannot fetch the catalog.**

---

## Step 3 — Create a GitHub Release and upload libs

### 3.1 Prepare files on your PC

Example for BGMI version `4.4.0`:

```text
libUE4.so
libanogs.so
```

(Use the real original offline libs for that game version.)

### 3.2 Create the Release

1. Repo → **Releases** → **Create a new release**  
2. **Tag:** `bgmi-4.4.0` (must match what you put in manifest later)  
3. **Title:** `BGMI 4.4.0 reference libs`  
4. Attach files:
   - `libUE4.so`
   - `libanogs.so`  
5. Publish release  

### 3.3 Copy direct download links

On the release page, right‑click each file → **Copy link address**.

Typical format:

```text
https://github.com/YOUR_USER/ue4dumper-catalog/releases/download/bgmi-4.4.0/libUE4.so
https://github.com/YOUR_USER/ue4dumper-catalog/releases/download/bgmi-4.4.0/libanogs.so
```

Test each link in a browser — download should start (or show a raw file).  
**Do not use the “html” release page URL.** Use the `/releases/download/...` URL.

---

## Step 4 — Put those links into `manifest.json`

Edit the BGMI `4.4.0` entry:

```json
{
  "versionName": "4.4.0",
  "versionCode": 0,
  "libs": [
    {
      "id": "ue4",
      "fileName": "libUE4.so",
      "label": "libUE4.so (BGMI 4.4.0)",
      "downloadUrl": "https://github.com/YOUR_USER/ue4dumper-catalog/releases/download/bgmi-4.4.0/libUE4.so",
      "sizeBytes": 0
    },
    {
      "id": "anogs",
      "fileName": "libanogs.so",
      "label": "libanogs.so (BGMI 4.4.0)",
      "downloadUrl": "https://github.com/YOUR_USER/ue4dumper-catalog/releases/download/bgmi-4.4.0/libanogs.so",
      "sizeBytes": 0
    }
  ]
}
```

Commit the change.

**Important:** `versionName` should match what Android shows as the **installed** game version  
(Settings → Apps → BGMI → version), e.g. `3.9.0` not only marketing names.

---

## Step 5 — Repeat for more versions

| Game | Example tags |
|------|----------------|
| BGMI 4.5.0 | `bgmi-4.5.0` |
| PUBGM 4.4.0 | `pubgm-4.4.0` |

Each version = **one Release** + **one `versions[]` block** in the manifest.

---

## Step 6 — Connect the Android app

See [06-connect-app.md](06-connect-app.md).

Short version:

1. Install the APK  
2. Accept agreement  
3. On **Environment setup**, paste raw manifest URL  
4. **Fetch server**  
5. **Download matching pack** for the game installed on the phone  

---

## Checklist

- [ ] Repo created and public  
- [ ] `manifest.json` on `main`  
- [ ] Raw URL opens in browser  
- [ ] At least one Release with `.so` files  
- [ ] `downloadUrl` values use `/releases/download/...`  
- [ ] `versionName` matches real installed game version  
- [ ] App fetch + download works  

---

## Next

→ [03-manifest-schema.md](03-manifest-schema.md)
