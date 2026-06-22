---
name: ask-neila
description: "Read a file — PDF, PowerPoint, Excel, image/photo, or text — or a whole folder of files, and explain it as an easy-to-understand colorful picture where alien characters break the concepts down. For a folder, Neila maps how the files connect and explains the through-line. Acts as a tutor: regenerate a different way when the user is stuck, dial depth from kid to expert, answer 'why?' follow-ups, offer alternative analogies, and export AI-readable markdown or a one-page cheat-sheet. Use when the user types /ask-neila, points at a file or folder to explain, asks to 'explain this simply', 'make this into a drawing', 'explain like I'm five', 'I don't understand this', or wants the files in a folder connected and explained."
---

# /ask-neila

**Point Neila at a file (or a whole folder) and she explains it.** She reads `.txt/.md/.pdf/.pptx/.xlsx/.csv` files and **photos/images**, then turns the hard concepts into a single colorful picture where friendly alien characters explain them in dead-simple language. Pasted text works too, but **reading files is the main job.**

Give her a **folder of files** and she goes further: she builds a little map in her head of how the files connect — shared ideas, what builds on what — and explains the whole thing *and* how the pieces fit together.

The user downloads the picture, and can also export the explanation as an **AI-readable markdown file** so other models can consume the simplified concepts too.

The real value is the **simplification** (plain words + a concrete analogy per concept). The aliens are the wrapper that makes it stick.

## Usage

```
# Main job — read a file:
/ask-neila path/to/file.pdf              # explain a PDF (incl. scanned)
/ask-neila path/to/slides.pptx           # explain a PowerPoint
/ask-neila path/to/data.xlsx             # explain a spreadsheet (or .csv)
/ask-neila path/to/photo.jpg             # explain a photo / image / screenshot
/ask-neila path/to/notes.md              # explain a markdown/text file

# Folder — connect the dots across many files:
/ask-neila path/to/folder/               # read every file, map how they connect, explain the whole

# Also works on pasted text:
/ask-neila <paste a paragraph here>

# Add-ons:
/ask-neila path/to/file.pdf --md         # also export an AI-readable .md
/ask-neila path/to/folder/ --cheatsheet  # also make a dense one-page revision sheet
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

## Keep it cheap

A picture is worth drawing once, not every time at full cost. Default to the cheapest version that still meets [QUALITY.md](QUALITY.md) and [EXPLAIN.md](EXPLAIN.md):

- **3–4 concepts**, not 6, unless the source clearly needs more.
- **Static by default.** Only add SVG animation if the user asks for motion — it's pure extra output tokens for a picture that's downloaded as a still anyway.
- **Mini-icon guests for posters/lists** (a circle + 2 eye-dots + one feature, ~10 lines of SVG) instead of full multi-part bodies. Full hand-drawn guest bodies are for comic panels where the guest is actually acting something out.
- **No filler decoration** (floating coins, sparkles, background clutter) unless it's load-bearing for the concept.
- **Don't re-read** [characters.md](characters.md), [cast.md](cast.md), [EXPLAIN.md](EXPLAIN.md), [QUALITY.md](QUALITY.md), or call `mcp__visualize__read_me` again if you already loaded them earlier in this same conversation — reuse what you remember.

## Process

1. **Get the content.** If the path is a **folder**, jump to the [Folder mode](#folder-mode--connect-the-dots-across-files) section below. For a single file or pasted text:
   - Pasted paragraph → use as-is.
   - `.txt` / `.md` / `.csv` → read it directly.
   - `.pdf` → use the `anthropic-skills:pdf` skill to extract text (it OCRs scanned PDFs too).
   - `.pptx` → use the `anthropic-skills:pptx` skill to extract text.
   - `.xlsx` / `.xls` → use the `anthropic-skills:xlsx` skill to read the data. Explain what the sheet *means* (the trends, relationships, what the numbers are telling you), not a cell dump.
   - **Photo / image** (`.png/.jpg/.jpeg/.webp/.gif`) → `Read` the file directly; Claude sees it natively. Works for diagrams, handwritten notes, screenshots, photographed textbook pages, whiteboards. Extract the concepts from what's in the image.

2. **Distill 3–4 concepts (see [Keep it cheap](#keep-it-cheap); up to 6 only if the source clearly needs it) so a 10-year-old gets them instantly.** This is the real product — the art only delivers it. **[EXPLAIN.md](EXPLAIN.md) is the standard — follow its six-beat method and run its pre-flight checklist before you draw anything.** In short, each concept gets: an **anchor** to something the kid already knows → a **plain name** (zero unexplained jargon) → the idea **in one concrete breath** → an **analogy that structurally maps** (note where it breaks) → a **tiny picturable example** → **why they'd care**. Run the curse-of-knowledge sweep and the explain-it-back test. Cut mercilessly: 3–4 well-built concepts beat 6 rushed ones. A muddy explanation cannot be rescued by a pretty picture.

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
   - **Before rendering, run the text-width and overlap checks from QUALITY.md §8 on every line and every element pair.** This is what catches text spilling past a card edge or an icon landing on top of a line — compute it, don't eyeball it.

5. **Render + deliver.** See [Rendering](#rendering--works-in-claude-code-and-claudeai-chat) for the platform-specific step. Either way:
   - Give it a specific topic-based name (e.g. `photosynthesis_explained`) — the `show_widget` title, or the artifact's implied filename.
   - The user gets a downloadable picture file either way.
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

## Folder mode — connect the dots across files

When the user points Neila at a **folder**, she doesn't just explain each file in isolation — she works out how they fit together and explains the *whole*.

1. **Read every supported file** in the folder (same readers as step 1: pdf, pptx, xlsx, images, text). Skip unsupported files and say which you skipped.

2. **Build the connection map.** Choose by size:
   - **A handful of files (≲ ~8):** do it in-context. For each file, pull its main idea(s); then find the links — shared concepts, what builds on what, cause→effect across files, agreements and contradictions. You're looking for the *through-line*: what story do these files tell together?
   - **A large folder, or the user wants a persistent/queryable graph:** delegate to the `graphify` skill (it's built exactly for this — folder → knowledge graph with clusters, hub concepts, and connection edges). Use its output as the map. Don't rebuild a graph engine. (`ask-neila: graphify does folder→graph; reuse it rather than reinventing clustering`)

3. **Draw the concept map** as the picture. This is a connection diagram, not a comic: each **node** is a key idea (or a file), **edges** show how they link (labelled with the relationship — "leads to", "is an example of", "contradicts"). Neila stands beside the map presenting it; guest aliens sit at the important hub nodes. Read the `diagram` module via `mcp__visualize__read_me` for this layout, and still hold to [QUALITY.md](QUALITY.md). Keep it legible — cluster related nodes, don't draw a hairball.

4. **Explain the through-line, simply.** Lead with the big picture in one or two plain sentences ("These five files are all about how a plant turns sunlight into food — each one covers a different step"). Then walk the map: each cluster/hub gets the EXPLAIN.md treatment, and call out the *links* explicitly ("this is why file 2 matters — it feeds into file 4"). The point of folder mode is the connections, so make them the star.

5. **Exports** work the same: `--md` writes the map + explanations as structured markdown; `--cheatsheet` condenses the whole folder to one page.

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

## Rendering — works in Claude Code AND claude.ai chat

This skill runs the same everywhere; only the render step differs by platform:

- **Claude Code (this CLI):** call `mcp__visualize__read_me` with `modules: ["art"]` (and `["diagram"]` for comic panels) **once** before your first `show_widget` call, then deliver via `mcp__visualize__show_widget`. Don't narrate the `read_me` call.
- **claude.ai chat, Desktop, or anywhere without those tools:** skip `read_me`/`show_widget` entirely — just output the finished SVG as a fenced ` ```svg ` code block in your reply. claude.ai turns this into a viewable, downloadable Artifact automatically. [QUALITY.md](QUALITY.md) and [characters.md](characters.md)/[cast.md](cast.md) are self-contained (hardcoded hex, no host CSS variables needed), so the picture looks identical either way.
- **File reading & folder mode:** use whichever file-ingestion the platform gives you — Claude Code's named skills (`pdf`/`pptx`/`xlsx`) if present, or just read an attached/uploaded file directly if the platform already extracted it into context (claude.ai does this automatically for PDF/DOCX/PPTX/XLSX/images on upload). The `graphify` skill (folder mode's big-folder path) is Claude Code-only — if it's not available, just use the in-context connection-map method regardless of folder size.

## Content boundaries

- **No sexual or explicit content, ever — with one narrow exception:** genuine biology/health education (e.g. human reproduction, puberty, anatomy, STIs covered in a school curriculum). Even then, stay clinical and diagrammatic — labelled body parts in the existing friendly-alien/cartoon style, the same bar a school textbook illustration uses. Never anatomically explicit, sexualized, or graphic.
- If a request is ambiguous about which case it falls into, ask before drawing rather than guessing.

## Notes / deliberate limits

- No real video — the user chose a picture file. Motion is gentle SVG animation, baked flat on download. (`ask-neila: picture-only by design; revisit if the user actually wants MP4`)
- No external image-generation API — hand-drawn SVG is free, instant, and keeps Neila and Pip consistent. (`ask-neila: SVG over image-gen for consistency + zero cost`)
- Image and scanned-doc reading uses Claude's native vision / the `pdf` OCR — no separate OCR dependency. (`ask-neila: native vision over a bolted-on OCR lib`)
