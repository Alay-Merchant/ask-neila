---
name: ask-neila
description: "Turn any paragraph, file, PDF, or PowerPoint into an easy-to-understand colorful picture where alien characters explain the concepts. Use when the user types /ask-neila, or asks to 'explain this simply', 'make this into a drawing', 'explain like I'm five with pictures', or wants a visual/illustrated explainer of some text or document."
---

# /ask-neila

Turn any input — a pasted paragraph, or a `.txt/.md/.pdf/.pptx` file — into a single colorful picture where friendly alien characters explain the hard concepts in dead-simple language. The user downloads the picture.

The real value is the **simplification** (plain words + a concrete analogy per concept). The aliens are the wrapper that makes it stick.

## Usage

```
/ask-neila <paste a paragraph here>      # explain pasted text
/ask-neila path/to/file.pdf              # explain a PDF
/ask-neila path/to/slides.pptx           # explain a PowerPoint
/ask-neila path/to/notes.md              # explain a markdown/text file
```

## The cast (keep these CONSISTENT every time)

**Neila** — the host. A small round teal alien (`#3FBFB0` body), **three eyes** in a row, two stubby antennae with round tips, a wide friendly smile, short arms. She always points at things and does the explaining. "alien" backwards.

**Pip** — Neila's alien dog. Smaller, lavender/purple (`#B59FE6`), **one big eye**, two floppy antennae for ears, a stubby tail, four little legs. He reacts to each concept (happy, confused, amazed) — comic relief and a visual anchor in every panel.

**Guest aliens, pets & animals** — pick ONE per concept from the cast in [cast.md](cast.md), matched to the concept by its "best for" column (e.g. `Quib` for chemistry, `Gravix` for gravity). If nothing fits, roll a new one from the forge parts in that file. Guests are NOT recurring and NOT teal/lavender (those are reserved for the stars).

Reusable SVG groups for Neila and Pip live in [characters.md](characters.md) — paste them in and reposition/recolor expressions rather than redrawing from scratch. This is what keeps the mascots recognizable across pictures. The 100+ guest roster and the mix-and-match part library live in [cast.md](cast.md).

## Process

1. **Get the text.**
   - Pasted paragraph → use as-is.
   - `.txt` / `.md` → read it.
   - `.pdf` → use the `anthropic-skills:pdf` skill to extract text.
   - `.pptx` → use the `anthropic-skills:pptx` skill to extract text.
   - Scanned/image-only PDFs and raw images are NOT supported in this version — tell the user plainly if you hit one.

2. **Distill 3–6 concepts so a 10-year-old gets them instantly.** This is the real product — the art only delivers it. **[EXPLAIN.md](EXPLAIN.md) is the standard — follow its six-beat method and run its pre-flight checklist before you draw anything.** In short, each concept gets: an **anchor** to something the kid already knows → a **plain name** (zero unexplained jargon) → the idea **in one concrete breath** → an **analogy that structurally maps** (note where it breaks) → a **tiny picturable example** → **why they'd care**. Run the curse-of-knowledge sweep and the explain-it-back test. Cut mercilessly: 3–4 well-built concepts beat 6 rushed ones. A muddy explanation cannot be rescued by a pretty picture.

3. **Pick the layout from the content** (don't ask):
   - **Comic strip / panels** — for sequential or process content (steps, cause→effect, how-something-works). Neila walks Pip through panel by panel.
   - **One poster** — for overview/list/definition content (a topic broken into parts). One scene, concepts arranged around the page, Neila pointing at each.

4. **Draw one colorful SVG to a world-class bar.** Build it for the `visualize` tool's `show_widget` (SVG mode). **[QUALITY.md](QUALITY.md) is the standard — read it before drawing and run its pre-flight checklist before you finalize.** The essentials it covers:
   - Composition: one focal point per panel, varied shot scale, rule of thirds, clear gutters, breathing room.
   - Color: one cohesive palette per picture (not a rainbow), characters readable against their backgrounds.
   - Typography: load the real Fredoka font; bubble text has a bold concept-title over a lighter one-liner.
   - Acting: eyes look at what they reference, bodies lean and gesture, Pip reacts differently each panel, guests physically embody their concept.
   - Show the analogy as a tiny **drawing**, not just words.
   - Motion: eased (keySplines), staggered, seamless loops, ≤3 movers, calm — and the frozen frame must look composed too.
   - Neila hosts every picture; Pip appears and reacts in every picture; one guest per concept acts it out.

5. **Render + deliver.** Call `mcp__visualize__show_widget`:
   - `title`: a specific snake_case name of the topic (this becomes the download filename, e.g. `photosynthesis_explained`).
   - The widget renders inline and gives the user a **download button** → that's their picture file.
   - Briefly, in text, also list the concepts + analogies so they have the words even without the image.

6. **Offer to save to the vault** (optional, ask): write the `.svg` into the user's Obsidian vault if they want to keep it.

## Before drawing, read the visualize guide

Call `mcp__visualize__read_me` with `modules: ["art"]` (and `["diagram"]` if the layout is comic panels) **once** before your first `show_widget` call, so you follow its CSS-variable and layout rules. Don't narrate that call.

## Notes / deliberate limits

- No real video — the user chose a picture file. Motion is gentle SVG animation, baked flat on download. (`ask-neila: picture-only by design; revisit if the user actually wants MP4`)
- No external image-generation API — hand-drawn SVG is free, instant, and keeps Neila and Pip consistent. (`ask-neila: SVG over image-gen for consistency + zero cost`)
- No OCR for scanned docs in v1 — add only if a real scanned-PDF case shows up.
