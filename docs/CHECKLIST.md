# Server implementation checklist

Print or tick this when setting up.

## Repo

- [ ] GitHub account ready  
- [ ] Repo `ue4dumper-catalog` created (**public**)  
- [ ] `manifest.json` on branch `main`  
- [ ] Raw URL opens in browser  

Raw URL:

```text
https://raw.githubusercontent.com/________/ue4dumper-catalog/main/manifest.json
```

## First release (example BGMI)

- [ ] Tag name: `bgmi-________`  
- [ ] Uploaded `libUE4.so`  
- [ ] Uploaded `libanogs.so`  
- [ ] Direct download URLs copied (`/releases/download/...`)  
- [ ] URLs pasted into `manifest.json`  
- [ ] `versionName` equals phone App info version: `________`  
- [ ] Committed to `main`  

## PUBGM (optional second game)

- [ ] Release tag `pubgm-________`  
- [ ] Libs uploaded  
- [ ] Manifest entry for `com.tencent.ig`  

## App

- [ ] APK installed  
- [ ] Agreement accepted  
- [ ] Manifest URL entered  
- [ ] Fetch server OK  
- [ ] Installed version shown correctly  
- [ ] Download matching pack OK  
- [ ] Files exist under `/sdcard/UE4Dumper/reference/...`  
- [ ] Finish setup  

## Optional

- [ ] `DEFAULT_MANIFEST_URL` set in `AppPrefs.kt`  
- [ ] APK update entry in `appUpdate`  
- [ ] SHA-256 filled for each lib  

## Need help from developer?

Send:

1. Your raw `manifest.json` URL  
2. One working release download URL  
3. Screenshot of BGMI/PUBGM **App info → version**  
