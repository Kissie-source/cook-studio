# Changelog — Cook Studio

Every version is a full snapshot in `versions/index-vX.Y.html` (and a git commit).
**Roll back:** copy the snapshot over `index.html`, re-upload to GitHub.

## v3.9 — 2026-11-22
- **Fix: pasting Claude's polish reply failed with "couldn't read that".** The reader now
  finds the suggestions whatever the Claude app wraps them in: a code block, chat text before
  or after (even text with brackets in it), `{"suggestions": [...]}`, curly quotes from the
  phone, or a reply cut off before its last bracket. If it still finds nothing, it says how
  to copy the whole answer.

## v3.8 — 2026-11-22
- **Studio steps reorder by dragging.** The ▲▼ buttons on the step rows are gone; each row
  has the same grip handle as the carousel list — hold it and drag the step to its place.
  Times, notes and photos travel with the step. With only one step there is no handle.

## v3.7 — 2026-10-25
- **The key prompt explains itself.** Asking for the API key now says what it is: made at
  console.anthropic.com as a developer account with credit, *not* the Claude app login,
  about 2 cents per photo, kept on the phone — and that cancelling leaves the no-key
  "via Claude app" route. The same wording sits under the cast buttons and on the polish field.

## v3.6 — 2026-10-25
- **"Via Claude app" now carries the prompt too.** Phones drop the text when a file rides
  along in the share sheet, so the photo goes through the sheet and the prompt is put on
  the clipboard at the same time — one paste at the other end. The two buttons also say
  what they do now: **fill it in** (here in the app, needs your key once) and
  **via Claude app** (no key).
- **Comments are set in Cormorant Garamond**, a little larger and heavier so the serif
  holds up at slide size. The font picker is gone.
- **A step you added but never ran keeps its place without inventing time.** It no longer
  gets a made-up second, it is left out of the donut and the legend, and the method slide
  shows it with a dash instead of a duration.

## v3.5 — 2026-10-24
- **Fix: steps added mid-cook were thrown away.** Anything added with "+" is now kept
  through to the Studio even if you never reach it (a step with no time counts as one
  second, so the charts still add up). Previously only steps with recorded time survived.
- **Send to Claude.** Next to the sparkle there is now a one-tap handoff: the ingredients
  photo *and* the prompt go to the Claude app through the phone's share sheet — no API
  key, no hunting in the gallery. On a desktop it copies the prompt and opens Claude.
- **Time slide, reworked.** Only the rushed round recorded → the plain donut with the
  total in the centre. Both rounds recorded → the nested ring, with RUSHED and SLOW
  underneath joined by a thin arrow carrying "4.3× of slow version", pointing at the slow
  time. Labels and figures are ink and grey now — colour belongs to the chart, not the type.
- **The comment moved above the chart** and can wear one of three serifs: **Fraunces**,
  **Cormorant Garamond** or **EB Garamond** (house sans stays the default). The ring drops
  to clear however many lines the comment runs to.

## v3.4 — 2026-10-24
- **Ingredient extraction stays in the app.** The copy-paste detour is gone — one tap on
  the sparkle, the key is asked for once and kept on the device. The prompt now also reads
  German kitchen shorthand: EL → tbsp, TL → tsp, Prise → pinch, Msp. → knife tip, Bund →
  bunch, and it keeps the qualifier ("1 kleiner EL" → "1 small tbsp").
- **Photo shapes.** In the photo editor: full slide (as before) or a card in 4:5, 1:1, 4:3,
  16:9 or 3:4. The crop preview takes the chosen shape, and a card sits centred on cream
  with the step name under it.
- **Strict palette.** Every colour literal is now navy · coral · cream · grey or a tint of
  them — the sage green (SLOW button, badges) and the leftover warm-brown shadows and
  off-whites are gone.
- **Another round of a step, mid-cook.** A "+" next to the camera inserts "MEP 2" (then
  "MEP 3"…) right after the step you are on, so repeats get their own timing and notes.
- **No percentage beside the step sliders** — the share is already on the chart.
- **The line under the time chart is yours to write.** It is pre-filled with the sentence
  the app writes; type over it, or press "write it for me" to go back to the automatic one.

## v3.3 — 2026-10-24
- **Fix: nothing stored was reachable in the first moments after opening the app.** The
  photo/audio database opens asynchronously, and every read fired without waiting for
  it — so a session's photos could come up empty and a voice note refused to play.
  All blob reads and writes now wait for the database. This is the cause behind both
  "pics in saved sessions not visible" and "listening button not working".
- **Fix: the drag handle was invisible and therefore un-draggable** — the icon painter
  only matched `<i>` elements and the handle is a `<span>`, so it rendered as an empty,
  zero-width box. The handle is now drawn, sits at the **right end of every slide row**,
  and has a proper 34×34 touch target.
- A note that cannot be played now says "no sound" on the button instead of failing mutely.
- **Title pic no longer destroys the previous one.** Promoting a photo moves the outgoing
  title pic into the photo strip (and skips that if it was only a copy of a photo already
  there). Same when uploading a new one.
- **Ingredient extraction translates.** Labels in any language come back in English, with
  the amounts exactly as printed. Added a **no-API-key route**: copy the prompt, attach the
  photo in the Claude app, paste the reply back.
- **Framing is now direct.** The ↔ / ↕ / zoom sliders are gone: drag the photo to move it,
  pinch to zoom (mouse wheel on a desktop). Brightness, contrast, colour and warmth stay
  as sliders.
- **"Where the time went" is the nested ring** (steps as a donut, the same split again as a
  pie inside) for both rounds, with **three ways to show the totals**: beside the ring ·
  rushed vs slow (pulls the other round of the same dish and shows both) · under the ring
  (both totals and the multiplier, e.g. "4.3× the clock").

## v3.2 — 2026-09-19
- **Voice notes are now 12 s** (was 7 s) — one constant, `NOTE_SEC`, drives the timer, the
  on-screen indicator and the setup hint.
- **Fix: a note could be lost when the auto-stop and finishing collided.** The save reads
  the session *after* an async blob write, and if the cook ended in between, the write
  threw and the note vanished — silently, since the failure also left the stop promise
  unresolved (the "note saved" line never appeared). The recorder state is now captured
  up front, and an in-flight save is claimed the moment the recorder stops, so "next
  step" and "finish" wait for it. Verified with a deliberately slowed stop event: three
  steps, three notes, none dropped.

## v3.1 — 2026-09-19
- **Photo dots while timing.** The live step list now shows one coral dot per photo saved
  on that step, updating the moment you shoot — so you can see at a glance which steps
  are covered and which have nothing. Past 6 photos it collapses to a dot + "×9" so the
  row never wraps.
- Fixes from the icon sweep: the cast button was printing its own markup as text, and the
  mic glyph on "note saved" was never drawn.

## v3.0 — 2026-09-19
- **Fine-line icons everywhere.** Every emoji in the interface is now a stroked SVG on
  one weight (clock, camera, mic, play/stop, sparkle, star, pencil, check, chevrons,
  download, refresh…). The emoji step-icon picker is gone — it was decorative and never
  appeared on a slide.
- **Cover: time ring.** A thin circle holding the total time sits on the title photo
  (dark scrim + white ring so it reads on any picture); without a photo the ring sits
  beside "every second tracked · door to bowl".
- **Method slide.** "THE STEPS" is now METHOD: each step shows its duration (`4 min` /
  `45 s`) in coral on the left, a dot on a dotted vertical rail, then the step name.
  No more "01 / 02" numbering, no right-hand time column. Footer line: total, door to bowl.
- **Where the time went: donut.** The pie is now a donut with the total time and the round
  in the hole, and a dry one-liner underneath — e.g. "30% of the clock went to airfryer
  to 200 · 20% to recipe reading."

## v2.9 — 2026-09-19
- **Crash insurance for a running cook.** The phone reloading the page (screen lock,
  charging, memory pressure, Safari backgrounding the tab) used to wipe the session —
  timer, voice notes, photos, timestamps, all of it. The live session is now mirrored
  to localStorage on every change, every 3 s, and whenever the page is hidden. On the
  next open, the Cook tab shows **COOK IN PROGRESS** with dish, elapsed time, current
  step, and how many notes/photos are safe: **Resume** puts you straight back in with
  the clock still counting from the original start, the current step and its elapsed
  time, the cast panel (photo + typed buckets) and every note and photo intact.
  "Throw it away" deletes it and its blobs.
- The screen wake-lock is re-requested when the app comes back to the foreground, so a
  lock/unlock no longer leaves the screen free to sleep mid-cook.

## v2.8 — 2026-09-19
- **Navy & Coral is the one look.** The look picker is gone; slides always render in
  navy · coral · cream. The app chrome now lives in the same world (coral accent, navy
  ink and cook mode, cream paper), so the Studio and the slides match.

## v2.7 — 2026-09-18
- **Photo adjustments.** In the big view, tap "✎ adjust": ↔/↕ frame and zoom (previewed
  as the exact 4:5 slide crop, so a half-cut dish can be re-framed), plus bright,
  contrast, colour, warm. "✨ polish" applies the house look — a touch brighter, +8%
  contrast, +15% colour, gently warm: positive and energetic without the cheap punch.
  Adjustments are baked into the photo slides and follow a photo onto the cover.
- **New colour world.** App chrome moves to blush · royal blue · sage · graphite on warm
  porcelain; cook mode is a deep navy. The brown/orange is gone.
- **Three looks for the slides**, picked per session in the Studio ("LOOK"):
  Blush & Royal (default) · Silver (brushed-steel monochrome, metallic titles) ·
  Navy & Coral. Each has its own verdict slide and pie palette.
- Dev: `serve.ps1` gained a PUT /out/ endpoint to export rendered slides; `out/` is
  git-ignored.

## v2.6 — 2026-09-18
- **Brand line off every slide.** The top-left "PERFECTION À LA CARTE" is gone from the
  cover, cast, pie, steps and verdict slides too (learn had it removed in v2.4). The
  @handle in the footer and the dish/round label top-right stay.

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
