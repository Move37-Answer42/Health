# Wayne Fit

Personal fitness tracker and recipe library, built around shoulder rehab and a 4-phase progression plan.

Live: `https://<your-username>.github.io/<repo-name>/`

## What it does

**Today tab** — daily checklist (rotator cuff, walk, creatine, multivitamin), protein tracker (170g target), shoulder pain log, Sunday weigh-in, today's workout if it's a workout day.

**Workouts tab** — current phase indicator, Day A + Day B routines, daily rotator cuff sequence. Tap any exercise for a demo photo, form notes, common mistakes, and "More images" / "Watch video" links.

**Food tab** — 38 recipes covering quick weeknight meals, batch cooks, weekend / guest dinners, grill nights, and savory late-night snacks. Heavy on South African heritage (Lamb Korma, Bobotie, Durban Beef Curry, Frikkadel, Brown Onion Pot Roast), Wisconsin venison, and what's actually in the pantry. Includes a smart shopping list that separates staples (always on hand) from items to buy.

**Progress tab** — weight chart, 30-day consistency tracker, shoulder pain log, phase tracker.

## The shoulder context

This app exists because of an MRI in early 2025 showing mild supraspinatus tendinopathy with a tiny interstitial tear, anterior labral fraying, and a Type 2 acromion. The workout plan is built around self-directed rehab:

- **Phase 1 (Wks 1–3):** Foundation. No pressing, no overhead. Daily rotator cuff + 2x/week lower & arms.
- **Phase 2 (Wks 4–6):** Add pulling (inverted rows).
- **Phase 3 (Wks 7–9):** Reintroduce push-ups (wall → incline → floor).
- **Phase 4 (Wks 10+):** Light overhead pressing. Lateral raises skipped permanently.

Phase advances are manual — tap the up arrow on the Workouts tab when you're ready.

## How to use

1. Open the deployed URL on your phone
2. iPhone: Share button → "Add to Home Screen"
3. Tap the home screen icon — opens fullscreen, no browser chrome
4. All data saves to your device via `localStorage` (no cloud, no account)

Note: localStorage is per-device. If you want sync across phone + laptop later, swap in Firebase (similar to the Playoff Pools app).

## Files

- **`index.html`** — the entire app, single deployable file. ~650 KB (most of it is the 18 base64-inlined exercise demo images).
- **`wayne-fitness-app.jsx`** — readable source. Edit this if you want to make changes, then re-run the build to get a new `index.html`.

## Deployment

GitHub Pages is the easiest path:

1. Push this repo
2. Settings → Pages → Source: `main` branch, `/ (root)`
3. Wait 1-2 minutes
4. Visit `https://<your-username>.github.io/<repo-name>/`

Netlify Drop also works (drag `index.html` to https://app.netlify.com/drop).

## Tech notes

- **No build step at runtime.** JSX is pre-compiled at build time. The browser only loads React, ReactDOM, Tailwind from CDN — no Babel.
- **Three external scripts:** Tailwind CSS, React 18.3.1, ReactDOM 18.3.1 (all from `cdn.tailwindcss.com` and `cdnjs.cloudflare.com`).
- **Everything else inlined:** lucide icons (as SVG JSON), exercise demo images (as base64 JPEG), app logic.
- **Data persistence:** `localStorage` only. State shape lives in `DEFAULT_STATE` in the JSX source.

## Editing & rebuilding

The build pipeline lives in a Python script (`build_html.py`) that:
1. Reads `wayne-fitness-app.jsx`
2. Strips React + lucide imports
3. Pre-compiles JSX → JS via `@babel/standalone`
4. Injects the compiled JS into an HTML template along with the lucide icon SVG data and base64 exercise images
5. Writes `index.html`

If you want changes (new recipes, exercise tweaks, layout), edit the `.jsx` and rebuild.

## Equipment owned

Reflects what's actually in the house:
- Two 25 lb dumbbells
- 4 resistance bands (lightest → heaviest, up to 125 lb)
- Wall + floor space (planks, dead bugs, wall slides)

Each exercise card flags whether to use bands or dumbbells.
