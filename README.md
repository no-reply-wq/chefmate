# Chefmate ERP — Web App Portal

PWA wrapper that serves the Chefmate ERP (Google Apps Script) via a custom domain,
with full-screen app installation support on Android and iOS.

---

## What this does

- Wraps the Google Apps Script ERP at a clean company URL (`erp.chefmateindia.com`)
- Enables "Add to Home Screen" / PWA install with the Chefmate logo
- Opens full screen — no browser bar — feels like a native app
- Works on Android (Chrome / Brave) and iPhone (Safari)

---

## Folder structure
portal/
├── index.html ← Main page (iframe wrapper + PWA meta tags)
├── manifest.json ← PWA manifest (name, icons, display mode)
├── sw.js ← Service worker (required for install prompt)
├── CNAME ← GitHub Pages custom domain config
└── icons/
├── icon-192.png ← App icon (home screen, 192×192)
└── icon-512.png ← App icon (splash screen, 512×512)


---

## Setup steps

### 1. GitHub Pages
- Push this folder to your GitHub repo
- Go to repo **Settings → Pages**
- Set source branch to `main` (or `master`), folder to `/portal` or root
- GitHub will publish it at `https://yourusername.github.io/reponame`

### 2. GoDaddy DNS (custom domain)
- Log in to GoDaddy → DNS Management for `chefmateindia.com`
- Add a **CNAME** record:
  - **Name:** `erp`
  - **Value:** `yourgithubusername.github.io`
  - **TTL:** 600
- Wait 10–30 minutes for DNS to propagate

### 3. GitHub Pages custom domain
- In repo **Settings → Pages → Custom domain**
- Enter: `erp.chefmateindia.com`
- Check **"Enforce HTTPS"** (required for PWA install to work)

### 4. Update the Apps Script URL
- Open `index.html`
- Replace the `src` in the `<iframe>` with your actual Apps Script deployment URL:https://script.google.com/macros/s/YOUR_DEPLOYMENT_ID/exec

- 
---

## How to install the app on mobile

### Android (Chrome or Brave)
1. Open `erp.chefmateindia.com` in browser
2. Tap the 3-dot menu → **"Add to Home Screen"** or **"Install App"**
3. Tap **Install** — Chefmate icon appears on home screen
4. Open from home screen — launches full screen, no browser bar

### iPhone (Safari only)
1. Open `erp.chefmateindia.com` in **Safari** (must be Safari, not Chrome)
2. Tap the **Share** button (box with arrow)
3. Tap **"Add to Home Screen"**
4. Tap **Add** — Chefmate icon appears on home screen

> ⚠️ iPhone PWA install only works in Safari. Chrome/Brave on iOS cannot install PWAs.

---

## Updating the ERP

When you redeploy your Google Apps Script (new deployment URL):
1. Open `index.html`
2. Update the `src` attribute of the `<iframe>` to the new URL
3. Commit and push — GitHub Pages auto-publishes within 1–2 minutes

---

## Tech stack

| Layer | Technology |
|-------|-----------|
| ERP Backend | Google Apps Script (GAS) |
| ERP Frontend | HTML/CSS/JS served by GAS |
| Wrapper | Static HTML (iframe + PWA manifest) |
| Hosting | GitHub Pages |
| Domain | GoDaddy → CNAME → GitHub Pages |
| SSL | GitHub Pages auto HTTPS (Let's Encrypt) |

---

## Maintained by

**LRBC** — [lalitraj.com](https://lalitraj.com)  
For **Chefmate Technologies** — [chefmateindia.com](https://chefmateindia.com)
