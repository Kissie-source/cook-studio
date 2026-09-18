# Changelog — Cook Studio

Every version is a full snapshot in `versions/index-vX.Y.html` (and a git commit).
**Roll back:** copy the snapshot over `index.html`, re-upload to GitHub.

## v2.5 — 2026-09-18
- **Slide list: ▲▼ removed.** Drag ☰ is the one way to order slides now; the card heading
  says so. (Steps keep their arrows — no drag there yet.)

## v2.4 — 2026-09-18
- **▶ beside each step.** The voice note for a step now plays from a button right next to
  its name field, so you can listen while you write. A second tap stops it; tapping
  another note stops the first. Under the hood, notes and photos now follow their step
  by id (they used to follow its *position*, so reordering or dropping a step attached
  them to the wrong one). Existing sessions are migrated on open. Only notes from steps
  you removed still show in a separate "Voice notes" section — hidden otherwise.
- **Drag to reorder slides.** ☰ handle on every carousel row; works with a finger.
  ▲▼ stay as a fallback.
- **Learn slide:** the top-left brand line is gone — the handle is already bottom-right.
- **Any photo can be the title pic.** In the big view: "☆ make title pic". It copies the
  photo, so deleting the title pic later never deletes the photo itself.
- **Cast slide columns.** Amounts sit in a right-aligned gray column, ingredient names
  line up after it — per bucket. "500 g spaghetti", "3 eggs", "½ lemon" all parse; a
  line without an amount ("salt") sits flush with the names.
- Studio step row: ✕ moved to the end of the slider line so the name row never wraps.

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
