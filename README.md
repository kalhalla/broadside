# Broadside v3 — Deployment

## Before deploying

1. Open `index.html`
2. Find line: `const SUPABASE_ANON_KEY = 'YOUR_ANON_KEY';`
3. Replace `YOUR_ANON_KEY` with your actual Supabase anon key
4. That's it. Everything else is configured.

## Files

```
index.html      — The entire app (single file)
sw.js           — Service worker for PWA/offline
manifest.json   — PWA manifest
```

## You'll also need

- Your existing PWA icons (icon-192.png, icon-512.png) from the previous deployment
- Or generate new ones — the app works without them, you just won't get the home screen icon

## Deploy to Vercel

Replace the files in your existing GitHub repo and push:

```bash
cp index.html sw.js manifest.json /path/to/your/broadside-repo/
cd /path/to/your/broadside-repo
git add .
git commit -m "v3 — neumorphic letterpress redesign"
git push
```

Vercel auto-deploys from GitHub. Live in ~60 seconds.

## What's different from v2

- Neumorphic design with blind-embossed title
- Floating letter particle background
- Book cover fetched from Open Library API
- Redesigned share card with engraved B watermark
- BOOKS easter egg hidden in hero text
- Same backend: Supabase, Amazon Associates, fingerprinting, profanity filter, reports
