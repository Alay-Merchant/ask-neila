---
name: ask-neila
description: "Turn any paragraph, file, PDF, PowerPoint, Excel sheet, or photo into an easy-to-understand colorful picture where alien characters explain the concepts. Acts as a tutor: regenerate explanations a different way when the user is stuck, dial depth from kid to expert, answer 'why?' follow-ups, offer alternative analogies, and export an AI-readable markdown or a one-page cheat-sheet. Use when the user types /ask-neila, asks to 'explain this simply', 'make this into a drawing', 'explain like I'm five', 'I don't understand this', or wants a visual explainer of some text, document, spreadsheet, or image."
---

# /ask-neila

Turn any input — a pasted paragraph, or a `.txt/.md/.pdf/.pptx/.xlsx/.csv` file, or a **photo/image** — into a single colorful picture where friendly alien characters explain the hard concepts in dead-simple language. The user downloads the picture, and can also export the explanation as an **AI-readable markdown file** so other models can consume the simplified concepts too.

The real value is the **simplification** (plain words + a concrete analogy per concept). The aliens are the wrapper that makes it stick.

## Usage

```
/ask-neila <paste a paragraph here>      # explain pasted text
/ask-neila path/to/file.pdf              # explain a PDF (incl. scanned)
/ask-neila path/to/slides.pptx           # explain a PowerPoint
/ask-neila path/to/data.xlsx             # explain a spreadsheet (or .csv)
/ask-neila path/to/photo.jpg             # explain a photo / image / screenshot
/ask-neila path/to/notes.md              # explain a markdown/text file
/ask-neila path/to/file.pdf --md         # also export an AI-readable .md
/ask-neila path/to/file.pdf --cheatsheet # also make a dense one-page revision sheet
/ask-neila <topic> --level expert        # depth dial: kid | teen | expert
```

**After an explainer, just talk to Neila** (no flag needed):
- "I don't get it" / "explain it again" → she **regenerates with a different approach**.
- "explain it like I'm 5 / a teenager / an expert" → depth dial.
- "why?" on a concept → she goes one layer deeper.
- "give me another analogy" → two fresh ones from different domains.

## The cast (keep these CONSISTENT every time)

**Neila** — the host. A small round teal alien (`#3FBFB0` body), **three eyes** in a row, two stubby antennae with round tips, a wide friendly smile, short arms. She always points at things and does the explaining. "alien" backwards.

**Pip** — Neila's alien dog. Smaller, lavender/purple (`#B59FE6`), **one big eye**, two floppy antennae for ears, a stubby tail, four little legs. He reacts to each concept (happy, confused, amazed) — comic relief and a visual anchor in every panel.

**Guest aliens, pets & animals** — pick ONE per concept from the cast in [cast.md](cast.md), matched to the concept by its "best for" column (e.g. `Quib` for chemistry, `Gravix` for gravity). If nothing fits, roll a new one from the forge parts in that file. Guests are NOT recurring and NOT teal/lavender (those are reserved for the stars).

Reusable SVG groups for Neila and Pip live in [characters.md](characters.md) — paste them in and reposition/recolor expressions rather than redrawing from scratch. This is what keeps the mascots recognizable across pictures. The 100+ guest roster and the mix-and-match part library live in [cast.md](cast.md).

## Process

1. **Get the content.**
   - Pasted paragraph → use as-is.
   - `.txt` / `.md` / `.csv` → read it directly.
   - `.pdf` → use the `anthropic-skills:pdf` skill to extract text (it OCRs scanned PDFs too).
   - `.pptx` → use the `anthropic-skills:pptx` skill to extract text.
   - `.xlsx` / `.xls` → use the `anthropic-skills:xlsx` skill to read the data. Explain what the sheet *means* (the trends, relationships, what the numbers are telling you), not a cell dump.
   - **Photo / image** (`.png/.jpg/.jpeg/.webp/.gif`) → `Read` the file directly; Claude sees it natively. Works for diagrams, handwritten notes, screenshots, photographed textbook pages, whiteboards. Extract the concepts from what's in the image.

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

6. **Export an AI-readable markdown twin** (when `--md` is passed, or offer it otherwise). Write the explanation as a structured `.md` file next to the source (or to a path the user gives) named `<topic>-explained.md`. This is the picture's text twin: it lets *other AI models* ingest the simplified concepts, not just humans. Use exactly this structure so it parses cleanly:

   ```markdown
   # <Topic> — explained simply

   > Source: <file path or "pasted text">
   > Audience: 10-year-old level. Generated by ask-neila.

   ## TL;DR
   <2–3 plain sentences a 10-year-old could repeat>

   ## Concepts

   ### 1. <Plain name of concept>
   - **Anchor:** <familiar thing it connects to>
   - **In one breath:** <the core idea, one concrete sentence>
   - **Analogy:** <the mapping analogy> _(breaks down at: <where, if it matters>)_
   - **Example:** <one concrete, picturable instance>
   - **Why it matters:** <the hook>

   ### 2. <next concept>
   ...

   ## Glossary (jargon → kid-words)
   - **<term>:** <≤5-word plain definition>
   ```

   Each concept's five bullets come straight from the six-beat method in [EXPLAIN.md](EXPLAIN.md), so the markdown and the picture say the same thing.

7. **Export a one-page cheat-sheet** (when `--cheatsheet` is passed, or offer it). Write `<topic>-cheatsheet.md` — the *dense* opposite of the explainer: a packed, exam-ready reference, not a gentle walkthrough. Structure: a one-line "what this is", a **key terms** table (term → tight definition), the core concepts as terse bullets, must-know **facts/formulas**, **common mistakes**, and a single "remember this" takeaway. Offer to render it as a Neila-styled visual one-pager (color-coded boxes, printable) if they want.

8. **Offer to save the picture** (optional, ask): write the `.svg` into the user's Obsidian vault if they want to keep it.

## Tutor mode (after the first explainer — Neila is a teacher, not a one-shot)

Once an explainer exists, the user can keep working with Neila conversationally. Each of these reuses the [EXPLAIN.md](EXPLAIN.md) method.

- **"I don't get it" / regenerate.** Do NOT reprint the same words louder — **change strategy**. First, if useful, ask what's confusing (which concept, or all of it). Then pick a *different* tactic and try again:
  1. Swap to a completely fresh analogy from another everyday domain.
  2. Drop the depth one level (toward kid).
  3. Break the sticky concept into 2–3 smaller baby-steps (more panels, one idea each).
  4. Redraw the picture clearer — a different guest who embodies it better, a bigger focal point, fewer things per panel.
  5. Slow down to one concept at a time instead of all at once.
  Regenerate can target just the explanation, just the picture, or both. Every retry must *visibly change approach* — if it didn't land, doing the same thing again won't help.

- **Depth dial** (`--level kid|teen|expert`, or "explain like I'm…"). Same topic, re-pitched:
  - **kid** — the default ELI5 bar in EXPLAIN.md.
  - **teen** — real terms allowed but defined on first use; one step more abstract; assumes basic school knowledge.
  - **expert** — precise vocabulary, assumes background, skips the basics — but keeps the clarity and structure. Expert ≠ jargon soup.

- **Ask "why?"** — the user names a concept; Neila peels back one layer and stays concrete. Chainable, like a curious kid's why-chain, until they hit bedrock ("…and that's just how the universe is").

- **Alternative analogies** — "that didn't click?" → offer **two** more analogies for the same concept, each from a *different* domain (e.g. sport, cooking, money, video games), so at least one connects. Note where each breaks if it matters.

## Before drawing, read the visualize guide

Call `mcp__visualize__read_me` with `modules: ["art"]` (and `["diagram"]` if the layout is comic panels) **once** before your first `show_widget` call, so you follow its CSS-variable and layout rules. Don't narrate that call.

## Notes / deliberate limits

- No real video — the user chose a picture file. Motion is gentle SVG animation, baked flat on download. (`ask-neila: picture-only by design; revisit if the user actually wants MP4`)
- No external image-generation API — hand-drawn SVG is free, instant, and keeps Neila and Pip consistent. (`ask-neila: SVG over image-gen for consistency + zero cost`)
- Image and scanned-doc reading uses Claude's native vision / the `pdf` OCR — no separate OCR dependency. (`ask-neila: native vision over a bolted-on OCR lib`)
