# Riddles - Brain

Part of the **Riddles** brand (5-app family). See brand strategy in `../PLAN.md`.

## Brand Brief (the big picture)
**Riddles** is a brand umbrella over 5 separate Android puzzle apps — Brain, Maths, Fun, Words, Pics — published under one developer account so they read as one family (tree model: brand = trunk, each app = branch, same DNA, different content). The format is modeled on the proven **Math | Riddle and Puzzle Game** by Black Games (10M+ downloads, 100 levels, type-the-answer, ad-gated hints, 100% free).

**What we are building:** a single clean **template app**, then cloning it into the other repos by swapping content JSON + theme color + icon + name. Same code, 5 independent GitHub repos, 5 Play listings, cross-promoted via a "More Riddles →" section in each.

**Core loop (identical in all 5):** 100 sequential levels, ascending difficulty (no easy/med/hard labels) → see puzzle → type answer (no MCQ) → correct unlocks next level. Stuck → watch **3 rewarded ads** to unlock a hint; still stuck → **1 more rewarded ad** reveals the solution (user still types it to mark solved).

**Monetization:** ads only — rewarded (hints/solution), app-open, banner, interstitial (placement TBD). AdMob + GDPR consent. **No IAP, no premium, no subscriptions.**

**Data/Backend:** Firebase Analytics + Crashlytics only (5 separate projects), **no Firestore**. All user data (progress, settings, onboarding flag) **local-only via Hive** — no login, no cloud sync.

**Tech:** Flutter, **Android only**. Riverpod (state), Hive (local DB), go_router (nav), google_mobile_ads, firebase_core/analytics/crashlytics. Per-app: own applicationId, icon, name, accent color, content JSON, privacy-policy URL.

**Flow:** Splash → app-open ad → 3 animated game-styled onboarding screens (first run only) → home (level grid: locked/unlocked/solved + "More Riddles") → play screen. Plus settings (theme/sound/rate/share/privacy) and a rate-app popup every 3rd home visit.

**Goal/outcome:** ship 5 lightweight, offline, ad-funded puzzle apps fast by reusing one battle-tested template, building a recognizable brand family on the Play Store.

## This App
- **Category:** logic / lateral-thinking riddles.
- **Repo:** https://github.com/DEVENDRAP7/Riddles-brain.git
- **Package id (FINAL, permanent):** `com.devendrap7.riddles.brain`
- **Accent color:** purple. Glyph: brain.
- **Privacy policy URL:** https://devendrap7.github.io/Riddles-brain/privacy-policy.html (live, GitHub Pages).

## Brand Constraints (all 5 apps)
- Android only — no iOS.
- No login / signup. Progress local only.
- Splash → 3 animated game-styled onboarding screens (visual only, first run) → home.
- No premium plans / subscriptions. Ads only.
- Firebase Analytics + Crashlytics (own separate Firebase project + google-services.json). No Firestore.
- User data LOCAL only (Hive) — no cloud sync.
- AdMob: own App ID + own ad unit IDs (not shared with other apps).

## Core Loop (same across brand)
- 100 levels, sequential unlock, ascending difficulty (no easy/med/hard labels).
- See puzzle → type answer (no MCQ) → check.
- Hint: watch 3 rewarded ads → unlock hint.
- Solution: watch 1 more rewarded ad → shows answer, user still types it to solve.

## Monetization — Ads only (no IAP)
- Rewarded (hint/solution), app-open, banner, interstitial (placement TBD). AdMob + consent.

## Content — DONE
- `ProblemSet.md` (rewritten) + `content_levels.json` (build-ready) created.
- **100 unique single-word answers**, fill-in-blank ready: articles stripped (HOLE not "A hole"), zero duplicates, no multi-word, all A–Z uppercase. Letter counts range 3–10.
- Each level: `level`, `question`, `answer` (UPPERCASE), `hint`.
- Bands: classic riddles (1–25), everyday objects (26–50), nature & sky (51–75), weather/plants/creatures (76–90), adventure (91–100). Difficulty ascends; level number = order.

## Gameplay format — Fill-in-the-blank (Brain-specific)
- Show **blank tiles = number of letters** in the answer (`answer.length`).
- Player taps an on-screen **A–Z keypad** (same approach as the Maths number pad) to fill the tiles.
- **No system keyboard ever** — no TextField. Custom keypad + Backspace + CHECK only.
- Answer match: uppercase compare, strip spaces (answers already normalized).

## Stack
- Flutter, Riverpod, Hive, go_router, google_mobile_ads.

## Build Status
- [x] Content locked (100 unique single-word answers + JSON).
- [x] Input design locked (A–Z keypad, fill-in-blank, no system keyboard).
- [ ] App NOT scaffolded yet — clone from the Maths template (built first).

## Reference: Maths template (already built — Brain will clone it)
The Maths app is the working template. Brain reuses its structure, swapping accent
colour (purple), app name "Riddles - Brain", id `com.devendrap7.riddles.brain`,
content `content_levels.json`, and the number pad → **A–Z keypad + letter tiles**.
Template features built so far:
- Flutter, Android-only; 2 tabs (Home + Levels) via go_router ShellRoute, Play pushed on top.
- Home: animated title, progress badge, big PLAY → current level.
- Levels: 100-tile grid (solved=green ✓, current=yellow pulsing, locked=grey 🔒); next locks until current solved.
- Play: question card, **custom keypad (no system keyboard)**, hint → solution, confetti on solve, unlock next.
- Cartoon scene background: gradient sky, sun + rotating light rays, multiple drifting clouds, hills; two-frame palette that pans Home↔Levels.
- **Walking-human navbar** (transparent, merged into scene): procedural figure walks a road at the bottom, carries the active wooden signboard on his head, runs between Home/Levels boards on tab switch, faces travel direction.
- Progress stored locally via Hive. **No ads, no Firebase yet** (deliberately deferred for now).
- Deps: flutter_riverpod, hive/hive_flutter, go_router, google_fonts, flutter_animate, confetti.
