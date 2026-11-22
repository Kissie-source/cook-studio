# Cook Studio — progress, open issues, next steps

_Last updated: 2026-11-22 · shipped version: **v3.7** (commit `ff9b164`) · live and verified at
https://kissie-source.github.io/cook-studio/_

---

## What this is

A single-file web app (`index.html`, ~93 KB, no build step, no dependencies) for the
"cooked twice, timed" Instagram channel **@perfection.a.la.carte**. One dish is cooked
twice — once rushed against a clock, once slow — and each cook becomes an Instagram
carousel.

**The flow:** Cook tab (dish, round, steps, ingredients photo) → live timer screen
(per-step timing, 12 s voice note per step, photos) → Studio (adjust the time split,
photos, ingredients, learnings, verdict) → generated 1080×1350 slides → download and post.

## How it runs

| | |
|---|---|
| **Source** | `index.html` — markup, CSS and JS in one file |
| **Storage** | Sessions in `localStorage`; photos and audio as blobs in IndexedDB (`palc` → `blobs`) |
| **Slides** | Drawn on `<canvas>` at 1080×1350, downloaded as PNG |
| **Hosting** | GitHub Pages from `main` at `Kissie-source/cook-studio` |
| **Publish** | `git push` — live in ~40–60 s. No build, no CI |
| **Local dev** | `serve.ps1` (git-ignored, not uploaded) serves the folder at `localhost:8321`; it also accepts `PUT /out/<name>` so rendered slides can be exported for review. `out/` is git-ignored |
| **Rollback** | Every version is a full snapshot: `Copy-Item versions\index-vX.Y.html index.html`, then push |
| **History** | `CHANGELOG.md` — one entry per version, newest first |

## Design system

- **Palette (strict — nothing outside it):** cream `#FAF6F0` · navy `#14213D` ·
  mid-navy `#3D5A80` · coral `#E07A5F` · deep coral `#B85C45` · blush `#F2CFC2` ·
  grey `#8A8F98`. Cook mode is deep navy `#0F1A33`.
- **Type:** system sans throughout; **Cormorant Garamond** for slide comments only
  (loaded from Google Fonts).
- **Icons:** fine-line stroked SVGs, one weight, defined in the `IC` map and painted by
  `paintIcons()` into any element carrying `data-ic`.

## Where things live in `index.html`

| Area | Anchor to search for |
|---|---|
| Palette and icon set | `:root{`, `const IC=` |
| Live session persistence / resume | `saveLive`, `showResumeCard`, `resumeCook` |
| Recording | `NOTE_SEC` (12 s), `startRec`, `stopRec` |
| Blob storage | `dbReady`, `putBlob`, `getBlob` |
| Photo editor (pan, pinch, colour, shapes) | `lbDown`, `drawAdjusted`, `RATIOS` |
| Ingredient extraction | `castPromptText`, `aiExtractCast`, `sendCastToClaude` |
| Slides | `slCover`, `slCast`, `slPie`, `slSteps`, `slPhoto`, `slLearn`, `slCTA` |
| Carousel order (drag) | `renderPlan`, `planDragStart` |

---

## Open issues

### 1. "Fill it in" (in-app ingredient extraction) reportedly fails — cause unknown
**The blocker.** The user reports the sparkle button failing; the cause was never
captured. Most likely no Anthropic API key, or a key without credit — but unconfirmed.
The app now explains what the key is (v3.7) and shows the HTTP status on failure.
**To resolve:** tap it once and read the status line. `401` = wrong key · `400` = credit
or malformed request · `429` = rate limited. Workaround in place: **via Claude app**
(no key).

### 2. Unverified on the real phone
Everything below was verified only with synthetic events in a desktop browser:
- whether the Claude app appears in the iOS **share sheet**, and that the clipboard
  prompt survives the handoff;
- how **pinch-to-zoom and drag** feel on glass (the maths is right; the feel is not tested);
- whether recorded **voice notes play back** on the device — the format differs by browser
  (webm on Android/Chrome, mp4 on iOS). A "no sound" label appears if playback fails.

### 3. Timer throttling while the phone is locked
Browsers throttle timers in a backgrounded tab, so the 12 s auto-stop can stretch. The
note stores its true length, so nothing is mislabelled. Not fixed — probably unfixable
in a web app.

### 4. Smaller things
- **Studio step rows still use ▲▼**; only the carousel list has drag handles.
- **The polish feature still has a copy-paste fallback**; the equivalent route for
  ingredients was removed in v3.6. Inconsistent.
- **Cormorant loads from Google Fonts** — offline, slide comments fall back to Georgia.
- **Slides are portrait-only** (1080×1350). Photos can be cropped to other shapes, but the
  canvas itself is fixed.
- **Extraction uses `claude-opus-4-8`** (~2 cents per photo). Haiku would be ~5× cheaper
  and likely sufficient for reading a label.
- **`Stickers Kissie/`** sits untracked in the project — commit, ignore or move it.
- **No automated tests.** Verification is manual browser automation each time.

---

## Next steps

1. **Settle issue 1** — one tap, read the status line, then either fix the request or
   drop "fill it in" and keep the no-key route as the only path.
2. **Do one real cook end to end on the phone** and report what breaks. That single pass
   closes most of issue 2: share sheet, pinch, playback, 12 s notes, and lock/resume.
3. **Then, in rough order of value:** drag handles on Studio step rows · switch extraction
   to Haiku to cut cost · decide the `Stickers Kissie/` folder · make the polish route
   consistent with the ingredient one.

## Working agreement

- Changes are verified in the browser before shipping — rendered slides are exported to
  `out/` and reviewed as images, not assumed.
- Every version gets a `versions/index-vX.Y.html` snapshot, a `CHANGELOG.md` entry, a
  commit, and a push.
- Replies end with: file path · preview URL · version.
