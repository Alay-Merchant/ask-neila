# Quality bar — make every picture world-class

This is the rubric Neila renders against. Step 4 of [SKILL.md](SKILL.md) must satisfy all of it. The difference between a clip-art doodle and a world-class explainer is here. Read it before drawing; run the pre-flight checklist before finalizing.

## 1. Composition

- **One focal point per panel.** The eye should land somewhere first. Size, color, or position the key thing to win attention.
- **Vary shot scale across panels:** an establishing wide shot, then medium, then a close-up for the punchline. Don't draw every panel at the same zoom — that's the #1 amateur tell.
- **Rule of thirds.** Place characters and key objects off-center, near the third-lines, not dead-center every time.
- **Reading order is unambiguous:** left→right, top→bottom. Panels are clearly separated by gutters (even white space, ~16–24px). Number panels if order could be missed.
- **Breathing room.** Don't fill every pixel. Negative space makes the focal point pop.

## 2. Color

- **One cohesive palette per picture**, not a rainbow. Choose a background family + 2–3 character hues that harmonize. Pull from the [cast.md](cast.md) palette.
- **Per-panel background tints shift subtly** to signal progression (e.g. warm → cool as a process completes). Backgrounds are flat, never gradients.
- Characters pop against their background — never a teal alien on a teal panel. Check contrast.
- Reserve a single accent (the `#FFD23F` yellow or `#FF8FB1` pink) for the thing you want noticed.

## 3. Typography

- Load a real rounded display font, don't rely on Comic Sans fallback. Put this at the top of the SVG:
  ```svg
  <style>@import url('https://fonts.googleapis.com/css2?family=Fredoka:wght@400;500;600;700&amp;display=swap');
  .ttl{font-family:'Fredoka','Comic Sans MS',sans-serif;font-weight:600}
  .bdy{font-family:'Fredoka','Comic Sans MS',sans-serif;font-weight:400}</style>
  ```
  (`fonts.googleapis.com` is allowlisted by the widget.) Use `class="ttl"` / `class="bdy"`.
- **Hierarchy in every bubble:** concept NAME bold and larger (~17px) on top, the plain one-liner lighter (~14px) below. Never one undifferentiated block.
- Sentence case. Never below 13px. Generous line spacing (`dy` ≥ 1.3em). Left-align body text in wide bubbles; center short labels.

## 4. Speech & thought bubbles

- **Tail points at the speaker's mouth.** A bubble whose tail points nowhere reads as broken.
- Speech = bubble with a triangular tail. Thinking = cloud outline with small trailing circles. Use the right one.
- **Bubbles never cover faces** — neither the speaker's nor anyone they're talking to. Route them into empty space.
- Bubble has padding: text inset ≥12px from the bubble edge on all sides.

## 5. Acting (the characters must perform)

- **Eyes look at what they reference.** If Neila points at a diagram, her eyes track that way too. Dead-ahead eyes in every panel = lifeless.
- **Bodies lean and gesture.** Lean toward what excites them, back from what surprises them. Arms point, present, shrug.
- **Pip reacts differently each panel** — happy, confused, amazed, sleepy. He's the audience's emotional mirror; recycling one pose wastes him.
- Guest aliens *physically embody* their concept (a stretchy alien stretches; a split alien is mid-split), not just stand holding a prop.

## 6. Show the analogy, don't just write it

Each concept's analogy must appear as a **tiny concrete drawing**, not only words in a bubble. "Memory is like a desk" → draw the little desk with papers. The drawing is the point; the text labels it. A picture of words is not an illustrated explainer.

## 7. Motion (optional — only add if the user asks for animation; static is the default and cheaper)

- **Ease, don't lerp.** Add `keyTimes` + `keySplines` with `calcMode="spline"` for ease-in-out. Linear motion looks robotic.
  ```svg
  <animateTransform attributeName="transform" type="translate" values="0 0;0 -4;0 0"
    keyTimes="0;0.5;1" calcMode="spline" keySplines="0.4 0 0.6 1;0.4 0 0.6 1"
    dur="2.6s" repeatCount="indefinite"/>
  ```
- **Stagger** start times (`begin="0.3s"`, `0.6s`…) so things don't pulse in unison.
- **Seamless loops:** first and last `values` must match, or it jumps.
- **Subtle and few.** Idle bob (2.5–3s), occasional blink, antenna sway, one prop emphasis. Cap ~3 moving things at once. No fast jitter, no flashing — it must read as alive, not anxious.
- **The frozen frame must still be composed** — the downloaded still catches one moment, so no character should be mid-ugly-pose at rest. Design the resting state first, animate around it.

## 8. Text fit and overlaps — compute these, don't eyeball them

This is the most common failure mode (text spilling past a card edge, an icon sitting on top of a connector line, a label crossing another box) and the #1 thing that makes a render look unprofessional. Fix it with arithmetic, not a glance — **mandatory, not optional, on every render:**

- **Text width check, every line, before drawing it:** `width ≈ char_count × font_size × 0.6`. The available width is `box_width − left_inset − right_padding` (subtract any badge/icon column too). If `width` > available, the line is too long — shorten it now, don't shrink the font or let it run past the edge. Re-check after any coordinate change; a moved box invalidates the old budget.
- **Build a bounding-box list before you write the final SVG.** For every element that isn't text-on-a-line (every card, panel, character, guest, icon, bubble, decoration, and connector line/path), write down its **absolute** bounding box `(x_min, y_min, x_max, y_max)` — resolve any `transform="translate(...)"` / `scale(...)` into the final coordinates first; a box's local coordinates aren't the box's real position. For circles/ellipses use `cx±r, cy±r`. For a connector line/path, use the bounding box of its full stroke path, not just its endpoints.
- **Check every pair.** With that list, check every pair of elements that aren't deliberately layered (icon vs. connector line, text vs. badge, card vs. card, guest vs. neighboring card) for intersection. The only allowed overlaps are intentional ones: a label centered inside its own box, or an arrowhead/line-end touching the exact element it points to or originates from — touching, not cutting across or sitting inside the unrelated box. If anything else intersects, move it: shrink it, reposition it, reroute the line with a wider curve, or add a gutter. Re-run the check after every coordinate change.
- Do this pass *after* you've placed everything but *before* calling render — fixing overlap on a finished mental layout is cheap; fixing it after the user reports a bug is not.

## 9. Finish & accessibility

- `role="img"` + meaningful `<title>` and `<desc>` (first children of `<svg>`).
- These are physical-color scenes: **hardcode all hex** (don't mix in theme `c-*` classes) so nothing inverts oddly in dark mode.
- Tight viewBox (content bottom + ~24px). No element off-canvas, no unintended overlaps, thick consistent outlines (4px on bodies, 2–3px on details).

## Pre-flight checklist (run before finalizing EVERY render)

1. **Did you write down absolute bounding boxes for every element and check every pair for intersection, plus the text-width check on every line?** (§8 — this catches the most common bugs; do it before the rest of this list, and do NOT call `show_widget` until this passes.)
2. Is there one clear focal point per panel, and do shot scales vary?
3. One cohesive palette — every character readable against its background?
4. Real font loaded; bubble text has bold-title / light-line hierarchy?
5. Every speech tail points at its speaker; no bubble covers a face?
6. Do eyes/bodies actually *act* — looking and leaning, Pip varied?
7. Is each analogy *drawn*, not just written?
8. Static by default — only animated if the user asked for motion; if animated, is it eased, staggered, seamless, ≤3 movers, calm not jittery, with a good-looking resting frame?
9. role/title/desc present, all hex hardcoded, viewBox tight?

If any answer is "no", fix it before calling `show_widget`. World-class is the default, not the upgrade.
