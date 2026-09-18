# Changelog — Cook Studio

Every version is a full snapshot in `versions/index-vX.Y.html` (and a git commit).
**Roll back:** copy the snapshot over `index.html`, re-upload to GitHub.

## v2.3 — 2026-09-18
- **Photos open big.** Tap any Studio photo for a full-screen view with ‹ › to flip
  through, the step name as caption, and an in-carousel / excluded toggle that stays
  in sync with the carousel plan. Include/exclude from the grid is now the small
  corner dot. Cast photo and title pic open big too. Esc / arrow keys work on desktop.
- **Polisher writes in numbers & signs.** Digits not words, and compact signs where they
  read naturally: `<5 min`, `≈2×`, `−30%`, `200 °C`, `rushed → slow`, en-dash ranges.
  Capped at two signs per line so it stays a sentence, not a formula.
- **Cooking before Reset.** Standard steps are now Recipe Reading → MEP → Cooking →
  Reset (+ Plating on SLOW).
- **Your step list survives a RUSHED/SLOW toggle.** Add as many steps as you like;
  the mic records a fresh note for each. Only an untouched list resets to the standard.
- **Leaner Studio steps & pie.** Each step row is one compact card (▲▼ · icon · name ·
  ✕ · slider), pill inputs, one-line section heading, smaller pie. Six steps fit where
  four used to, without losing structure.
- **Fix:** slider math went negative on very short cooks (e.g. 6 s over 6 steps) — the
  minimum slice now scales with the total.

## v2.2 — 2026-08
- Cast photo can be taken on the setup card, before timer & mic start; carries into the
  session and follows you onto the live screen.
- AI extraction fixed: same model as Polish (`claude-opus-4-8`), on-device API-key
  prompt, HTTP errors surfaced, retry hint.

## v2.1 — 2026-08
- The Cast on the timer page: shoot ingredients while cooking; Claude vision fills the
  Soul / Aromatics buckets; manual editing; two-column cast slide.

## v2.0
- Salif editorial redesign — warm beige app, charcoal cook mode, orange slides.

## v1.0
- Neutral studio chrome, dark cook instrument, pastel Quicksand slides.
