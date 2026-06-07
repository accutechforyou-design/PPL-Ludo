# PPL Ludo — Pioneer LT 12 Setup Guide

## What you have
- `index.html` — Complete PWA app (all features built in)
- `manifest.json` — Makes it installable on iOS/Android
- `sw.js` — Offline support
- `icons/` — Put your PPL logo here as `ppl-logo.png`

---

## STEP 1: Add the PPL Logo

1. Copy your PPL logo image to the `icons/` folder
2. Rename it to `ppl-logo.png`
3. The app will automatically show it on the splash screen, login, and board

---

## STEP 2: Create Firebase Project

1. Go to **https://console.firebase.google.com**
2. Click **"Add project"** → name it `ppl-ludo-lt12`
3. Disable Google Analytics (not needed) → **Create project**

### Enable Firestore Database
1. Left sidebar → **Firestore Database** → **Create database**
2. Choose **Production mode** → select region (e.g., `asia-south1` for India)

### Enable Storage
1. Left sidebar → **Storage** → **Get started**
2. Choose **Production mode**

### Set Firestore Security Rules
Go to **Firestore → Rules** and paste:
```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if true;
    }
  }
}
```
*(This allows all reads/writes — fine for a closed group. Tighten later if needed.)*

### Set Storage Security Rules
Go to **Storage → Rules** and paste:
```
rules_version = '2';
service firebase.storage {
  match /b/{bucket}/o {
    match /{allPaths=**} {
      allow read, write: if true;
    }
  }
}
```

### Get Your Firebase Config
1. Go to **Project Settings** (gear icon) → **General**
2. Scroll to **"Your apps"** → click **"</>" (Web)** → register app as `ppl-ludo`
3. Copy the `firebaseConfig` object — it looks like:
```js
const firebaseConfig = {
  apiKey: "AIza...",
  authDomain: "ppl-ludo-lt12.firebaseapp.com",
  projectId: "ppl-ludo-lt12",
  storageBucket: "ppl-ludo-lt12.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abcdef"
};
```

### Update index.html with your Firebase config
Open `index.html` and find this section (around line 350):
```js
const FB_CFG={
  apiKey:"YOUR_API_KEY",
  authDomain:"YOUR_PROJECT_ID.firebaseapp.com",
  projectId:"YOUR_PROJECT_ID",
  ...
```
Replace with your actual values.

---

## STEP 3: Deploy to GitHub Pages

### Create the Repository
1. Go to **https://github.com/accutechforyou**
2. Click **New repository** → name it `ppl-ludo` (or `pioneer-lt12`)
3. Set to **Public** → **Create repository**

### Upload Files
Option A — GitHub web (easiest):
1. Open the repository → click **"uploading an existing file"**
2. Drag all files: `index.html`, `manifest.json`, `sw.js`, and the `icons/` folder
3. Click **Commit changes**

Option B — Git command line:
```bash
cd "E:\JBN Pioneer LT 11\PPL\Ludo\Pioneer Business League"
git init
git add .
git commit -m "PPL Ludo v1"
git remote add origin https://github.com/accutechforyou/ppl-ludo.git
git push -u origin main
```

### Enable GitHub Pages
1. Repository → **Settings** → **Pages** (left sidebar)
2. Source: **Deploy from a branch** → Branch: **main** → **/ (root)**
3. Click **Save**
4. Your site will be live at: `https://accutechforyou.github.io/ppl-ludo/`

---

## STEP 4: Share the Link

Send this to all PPL LT 12 members:
> **PPL Ludo App:** https://accutechforyou.github.io/ppl-ludo/
> 
> Open in Safari (iOS) or Chrome (Android) → tap the Share button → **"Add to Home Screen"** → it works like a real app!

---

## HOW MEMBERS LOG IN (First Time)

1. Open the app → tap **"First time? Set your password →"**
2. Select their name from the dropdown
3. Create a password (minimum 6 characters)
4. Done! They stay logged in for 30 days automatically.

---

## ADMIN ACCESS

These accounts automatically get admin access when they register:
- **Aakash Mehta** — Admin
- **Harshal Shah** — Admin
- **Manan Shah** — Admin
- **Abhishek Shah** — Admin
- **Dr. Vivek Mehta** — Admin
- **Srishti Shah** — **Master Admin** (can shuffle boards, full access)

After logging in, admins see a ⚙️ button (top right) to access the Admin Panel.

---

## DEMO ACCOUNTS

Two demo accounts are pre-built to show new members how the app works:
- Open app → scroll to **"Demo Accounts"** section → tap either button
- Demo sessions last 2 hours and show 10 pre-populated meetings

---

## ADDING NEW MEMBERS MID-SEASON

1. Log in as Admin
2. Tap ⚙️ → **Admin Panel** → **Add Member**
3. Enter name + select team → tap **Add Member**
4. The new member can then register with the login flow

---

## DOWNLOADING REPORTS

1. Log in as Admin → ⚙️ → **Admin Panel** → **Report**
2. Tap **"Download CSV Report"**
3. Opens a `.csv` file you can open in Excel/Google Sheets

The CSV shows: Date, From Member, From Team, To Member, To Team, Category, Points, Has Photo, Timestamp

---

## TROUBLESHOOTING

**App shows blank screen / Firebase error:**
- Check that you replaced all `YOUR_PROJECT_ID` values in `index.html`
- Make sure Firestore and Storage are enabled in Firebase console

**Photos not uploading:**
- Check Firebase Storage rules (must be `allow read, write: if true`)
- On iOS: allow camera/photo access in Settings → Safari → Camera

**Member not in dropdown:**
- Use Admin Panel → Add Member to add them

---

*Created by Srishti Shah, Abhishek Shah & Dr Vivek Mehta (Poppy)*
*Pioneer Power League — LT 12*
