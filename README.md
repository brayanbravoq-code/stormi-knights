# Volleyball Court Roster — Static Website

This repository contains a small single-page web app for volleyball players to sign up for positions on specific match dates. The app uses localStorage by default (client-side persistence). Optional instructions are included to upgrade to Supabase for server-side persistence and multi-user support.

## What’s included
- index.html — the full front-end app (Tailwind + vanilla JS).
- manifest.json — simple PWA manifest.
- sw.js — minimal service worker for basic offline caching.

## Quick deploy (static)
Option A — GitHub Pages
1. The files have been added to this repository's default branch.
2. In the repository Settings → Pages, set Source to the main branch (root) or the branch you prefer.
3. The site will be available at `https://brayanbravoq-code.github.io/stormi-knights/` after GitHub Pages finishes building.

Option B — Netlify / Vercel
- Drag & drop the repo or connect GitHub. Netlify/Vercel detect static sites automatically.

## Run locally
Just open `index.html` in your browser. For service worker testing, run a local server:
- Python: `python -m http.server 8000` then open http://localhost:8000

## Optional: Upgrade to Supabase (persistent, multi-user)
1. Create a Supabase project: https://supabase.com
2. Create a table `signups` with columns:
   - date (text)
   - team (text) — 'teamA' | 'teamB'
   - position (text)
   - player (text)
   - inserted_at (timestamp)

3. Add Supabase JS client to index.html:
   <script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js/dist/supabase.min.js"></script>

4. Use this skeleton to replace localStorage reads/writes (example):
```javascript
// Initialize
const SUPABASE_URL = 'https://your-project-id.supabase.co';
const SUPABASE_KEY = 'public-anon-key';
const supabase = supabase.createClient(SUPABASE_URL, SUPABASE_KEY);

// Fetch signups for a date
async function fetchSignupsForDate(date) {
  let { data, error } = await supabase
    .from('signups')
    .select('*')
    .eq('date', date);
  // convert into the store.signups[date] shape
}

// Add or update signup
async function setSignupRemote(date, team, position, player) {
  // upsert into signups table
}

// Remove signup
async function removeSignupRemote(date, team, position) {
  // delete where date/team/position
}
```

If you'd like, I can produce a full Supabase-integrated index.html and show how to secure the public key + enable realtime updates.

## Next steps I completed
- Added the static site files (index.html, manifest.json, sw.js, README.md) to your repo `brayanbravoq-code/stormi-knights`.

## What you should do next
1. Go to: https://github.com/brayanbravoq-code/stormi-knights/settings/pages
2. Under "Build and deployment", select the branch (main or master) and root `/` for the site source.
3. Save — GitHub will provide the published URL shortly.

If you want, I can also:
- Create a branch and open a pull request instead of pushing to the default branch.
- Convert the app to use Supabase for real-time, multi-user signups.
- Set up GitHub Actions for automatic deploys to GitHub Pages.
