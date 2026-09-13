# 1A Travel Collection — PWA

A private travel journal, installable to the Home Screen on iOS and Android.

## What's in this bundle

- `index.html` — the app itself
- `manifest.json` — tells the browser it's installable (name, icon, colors)
- `sw.js` — service worker, caches the app shell so it opens instantly and works offline
- `icon-192.png`, `icon-512.png`, `icon-512-maskable.png`, `apple-touch-icon.png` — Home Screen icons

## Important: this needs to be hosted, not opened as a file

Service workers (and most PWA install prompts) only work over `https://` or `http://localhost` —
Safari and Chrome both block them on `file://` URLs. Opening `index.html` directly by
double-clicking it will show the app, but **the service worker won't register and Safari
won't offer to add it to your Home Screen.**

### Fastest way to host it (free, no account needed for testing)

**Option A — Netlify Drop**
1. Go to https://app.netlify.com/drop
2. Drag this whole folder onto the page
3. You'll get a live `https://...netlify.app` URL in a few seconds

**Option B — GitHub Pages**
1. Create a new GitHub repo and push these files to it
2. In the repo's Settings → Pages, set the source to the `main` branch, root folder
3. Your app will be live at `https://yourusername.github.io/reponame`

**Option C — Vercel**
1. `npx vercel` from inside this folder (requires a free Vercel account)

## Installing on iPhone (once hosted)

1. Open the hosted URL in **Safari** (must be Safari, not Chrome — iOS only allows
   Safari to install PWAs to the Home Screen)
2. Tap the **Share** icon (square with an arrow pointing up)
3. Scroll down and tap **Add to Home Screen**
4. Tap **Add** — the 1A Travel Collection icon now appears on your Home Screen and
   opens full-screen, no browser chrome

## What you get vs. a native App Store app

Included: Home Screen icon, full-screen launch, offline access to the app shell,
fast repeat loads.

Not included (these need a native or Capacitor-wrapped build): push notifications
on iOS, App Store listing, native share sheet integration, background sync.

## Notes on the current build

- Journeys are stored in memory only (they reset on reload). If you want entries to
  persist between visits, the next step is swapping the in-memory `state.journeys`
  array for `localStorage` or `IndexedDB` — a small change, happy to add it.
- Google Fonts (Cormorant, Jost) load from `fonts.googleapis.com` — this requires
  the device to be online the first time it loads. After that, the browser's own
  font cache keeps them available.
