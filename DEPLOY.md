# DROPeZi – Firebase Deployment Guide

## Files in this folder
```
index.html        ← main website (single page)
logo.webp         ← compressed logo (10 KB, modern browsers)
logo.jpg          ← fallback logo (14 KB, older browsers)
firebase.json     ← Firebase hosting config
.firebaserc       ← Firebase project alias
```

---

## Step 1 — Install Firebase CLI (one-time)
```bash
npm install -g firebase-tools
```

---

## Step 2 — Login to Firebase
```bash
firebase login
```
This opens a browser window. Log in with the Google account that owns your Firebase project.

---

## Step 3 — Create a Firebase Project (one-time)
1. Go to https://console.firebase.google.com
2. Click **Add project** → name it `dropezi-website` (must match `.firebaserc`)
3. Disable Google Analytics (not needed for a static site) → **Create project**

---

## Step 4 — Deploy
```bash
cd /path/to/DROPeZi-Project-01
firebase deploy
```

You'll get a live URL like:
`https://dropezi-website.web.app`

---

## Step 5 — Connect dropezi.in custom domain

In Firebase console → **Hosting** → **Add custom domain**:

| Domain | Action |
|--------|--------|
| `dropezi.in` | Add & verify |
| `www.dropezi.in` | Add & verify |

Firebase gives you two **A records** (IP addresses). Add them in your domain registrar's DNS panel:

```
Type    Name    Value
A       @       151.101.1.195    (Firebase IP 1)
A       @       151.101.65.195   (Firebase IP 2)
CNAME   www     dropezi.in.
```

> ⚠️ Actual IPs are shown in the Firebase console after you add the domain — use those exact values.

SSL certificate is provisioned automatically (free, Let's Encrypt). Takes 15–30 minutes to go live.

---

## Step 6 — Map all 3 domains to the same project

Repeat the "Add custom domain" step for:
- `dropezi.com` → same DNS A records
- `dropezi.app` → same DNS A records

All three will serve the same `index.html` — no code changes needed.

---

## Future deploys

Any time you update `index.html` or `logo.webp`:
```bash
firebase deploy
```
Done. Changes go live in ~30 seconds globally.

---

## Quick DNS propagation check
```bash
# Check if your domain is pointing correctly
nslookup dropezi.in
# or
dig dropezi.in A
```
