# Broadside — Deployment Guide

## Files in This Repo

```
broadside/
├── index.html         # The complete app
├── manifest.json      # PWA manifest for home screen install
├── generate-icons.html # Open this to generate all icons
├── icon-16.png        # Generate these using generate-icons.html
├── icon-32.png
├── icon-180.png
├── icon-192.png
├── icon-512.png
├── og-image.png       # Social sharing image
└── README.md
```

---

## Quick Start (30 minutes total)

### Step 1: Generate Icons (2 min)

1. Open `generate-icons.html` in your browser
2. Click "Download All Icons"
3. Also click the OG Image to download it
4. Add all downloaded PNGs to this folder

---

### Step 2: Register Domain (5 min)

Go to [GoDaddy](https://www.godaddy.com/domainsearch/find?domainToCheck=broadside.press) and register **broadside.press**

---

### Step 3: Create Supabase Project (10 min)

1. Go to [supabase.com](https://supabase.com) and sign up (free)
2. Click "New Project"
3. Name it `broadside`
4. Set a database password (save this)
5. Choose region closest to you
6. Wait for project to spin up (~2 min)

**Create the table:**

1. Go to SQL Editor in sidebar
2. Paste this and click "Run":

```sql
create table recommendations (
  id uuid default gen_random_uuid() primary key,
  title text not null,
  reason text not null,
  fingerprint text,
  created_at timestamp with time zone default now()
);

-- Enable public read/write (for anonymous access)
alter table recommendations enable row level security;

create policy "Allow public read" on recommendations
  for select using (true);

create policy "Allow public insert" on recommendations
  for insert with check (true);
```

**Get your credentials:**

1. Go to Settings → API
2. Copy "Project URL" (looks like `https://xxxxx.supabase.co`)
3. Copy "anon/public" key (long string starting with `eyJ...`)

---

### Step 4: Amazon Associates (10 min)

1. Go to [affiliate-program.amazon.com](https://affiliate-program.amazon.com)
2. Sign up / sign in
3. Once approved, go to Account Settings
4. Find your "Tracking ID" (looks like `yourname-20`)

**Note:** Amazon Associates approval can take 24-48 hours. The site works without it—links just won't be tracked.

---

### Step 5: Configure the Code (2 min)

Open `index.html` and find these lines near the top:

```javascript
const USE_DEMO_MODE = true;
const SUPABASE_URL = 'YOUR_SUPABASE_URL';
const SUPABASE_ANON_KEY = 'YOUR_SUPABASE_ANON_KEY';
const AMAZON_AFFILIATE_TAG = 'YOUR_AMAZON_TAG-20';
```

Replace with your values:

```javascript
const USE_DEMO_MODE = false;  // ← Change to false!
const SUPABASE_URL = 'https://xxxxx.supabase.co';
const SUPABASE_ANON_KEY = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...';
const AMAZON_AFFILIATE_TAG = 'broadside-20';
```

---

### Step 6: Deploy to GitHub + Vercel (5 min)

**Push to GitHub:**

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/broadside.git
git push -u origin main
```

**Deploy on Vercel:**

1. Go to [vercel.com](https://vercel.com)
2. Click "Add New Project"
3. Import your GitHub repo
4. Deploy (takes ~30 seconds)

---

### Step 7: Connect Domain (3 min)

1. In Vercel, go to your project → Settings → Domains
2. Add `broadside.press`
3. Vercel will show you DNS records to add
4. Go to GoDaddy → DNS Settings
5. Add the records Vercel specifies
6. Wait 5-30 minutes for propagation

---

### Step 8: Seed Content (1 hour)

Before you launch publicly, add 30-50 quality recommendations. Quality seeds attract quality content.

---

## Adding to Home Screen (PWA)

**iPhone:**
1. Open broadside.press in Safari
2. Tap Share button
3. Tap "Add to Home Screen"

**Android:**
1. Open broadside.press in Chrome
2. Tap menu (three dots)
3. Tap "Add to Home Screen" or "Install App"

---

## You're Live!

**Marketing checklist (1 hour/day):**

- [ ] Share on book Twitter/Threads/Bluesky
- [ ] Post to r/suggestmeabook, r/books
- [ ] Reach out to book bloggers
- [ ] Create shareable cards using the Download button
