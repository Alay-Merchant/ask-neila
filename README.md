# 🛸 ask-neila

> Point it at a file — or a whole folder — and friendly alien characters explain it in dead-simple language as a colorful illustrated picture. Hand Neila a folder and she maps how the files connect and explains the whole story.

**ask-neila** is a [Claude Code](https://claude.com/claude-code) skill. **Its main job is reading your files** — PDFs, slides, spreadsheets, photos, notes — pulling out the few ideas that actually matter, rewriting each in plain words with a concrete analogy, and drawing a single picture you can download. Starring **Neila** the alien and her alien dog **Pip**, plus a cast of 100+ topic-themed guests. Pasted text works too, but files are the point.

The real value is the *simplification*. Neila is built on a strict pedagogy method ([EXPLAIN.md](EXPLAIN.md)) that turns expert jargon into something a 10-year-old explains back to a friend. The aliens are the wrapper that makes it stick.

## Example

**You give it this:**

> "Entropy is a measure of the number of microstates consistent with a given macrostate; the second law of thermodynamics states that the total entropy of an isolated system never decreases over time."

**Neila gives back this** (anchor → plain idea → analogy → why you'd care):

> 🛸 **Neila:** "You know how your room *never* tidies itself, but it gets messy on its own all the time? That's basically a law of the universe. **Entropy** is just a fancy word for 'how mixed-up and spread-out things are.' Left alone, everything drifts from tidy to messy — heat spreads out, smells fill the room, ice melts into a puddle. It can go the other way, but *only if someone does work* (you, tidying). That one-way drift is why time feels like it only goes forwards."

Same fact. One a 10-year-old repeats at dinner; the other they skip. Then it's drawn — Neila pointing at a messy room, Pip knocking over a tower, with the words in a speech bubble.

## What it does

```
/ask-neila <paste a paragraph here>      # explain pasted text
/ask-neila path/to/lecture.pdf           # explain a PDF (scanned too)
/ask-neila path/to/slides.pptx           # explain a PowerPoint
/ask-neila path/to/data.xlsx             # explain a spreadsheet (or .csv)
/ask-neila path/to/whiteboard.jpg        # explain a photo / screenshot / notes
/ask-neila path/to/notes.md              # explain a markdown/text file
/ask-neila path/to/folder/               # read a whole folder & connect the dots
/ask-neila path/to/lecture.pdf --md      # also export an AI-readable .md
```

**Inputs:** single files or a **whole folder** — text, `.md`, `.txt`, `.csv`, `.pdf` (incl. scanned), `.pptx`, `.xlsx`/`.xls`, and images (`.png/.jpg/.jpeg/.webp/.gif` — diagrams, handwritten notes, screenshots, photographed pages).

**Folder mode:** hand Neila a folder and she reads every file, builds a **map of how they connect** (shared ideas, what builds on what, contradictions), draws that map, and explains the *through-line* — the story the files tell together. For big folders she leans on the `graphify` skill rather than reinventing the graph.

**Outputs:** the **picture** (for humans), an optional **markdown twin** (for AIs), and an optional **one-page cheat-sheet** (dense, exam-ready revision reference).

## Tutor mode — Neila doesn't give up on you

Neila isn't a one-shot. After the first explainer, just talk to her:

- **"I don't get it"** → she **regenerates with a different approach** — a fresh analogy, a simpler level, smaller baby-steps, or a clearer redraw. Never the same words louder.
- **Depth dial** → "explain like I'm 5 / a teenager / an expert." Same topic, re-pitched to your level.
- **"Why?"** → pick a concept and she peels back a layer, staying concrete, as deep as you want to go.
- **"Another analogy?"** → two more from different everyday domains (sport, cooking, money…) so one is bound to click.

For each input, Neila:

1. **Extracts the text** (reusing Claude's built-in `pdf` / `pptx` skills for documents).
2. **Distills 3–6 core concepts**, each as a plain one-liner + an everyday analogy.
3. **Picks the layout from the content** — a comic strip for step-by-step ideas, one poster for overviews.
4. **Draws it** as a colorful animated SVG, held to a [world-class quality bar](QUALITY.md).
5. **Renders it inline** with a download button, so you walk away with the picture.

## The cast

- **Neila** — the host. A teal three-eyed alien ("alien" backwards) who does the explaining.
- **Pip** — her loyal one-eyed alien dog, who reacts to every concept.
- **100+ guests** — a parametric "alien forge" (bodies × eyes × antennae × limbs × props × hues) plus a named roster of explainers, pets, and wild alien animals, each tagged with what it's *best for*. Explaining gravity? Neila summons **Gravix**. Chemistry? **Quib**. See [cast.md](cast.md).

## Install

This is a Claude Code skill. Clone it into your skills directory:

```bash
git clone https://github.com/Alay-Merchant/ask-neila.git ~/.claude/skills/ask-neila
```

Then in Claude Code, type `/ask-neila` followed by your text or a file path.

> Requires the `visualize` tool (for rendering) and, for documents, the `pdf` / `pptx` skills. Scanned/image-only PDFs aren't supported yet.

## Files

| file | what it is |
|------|-----------|
| [SKILL.md](SKILL.md) | the pipeline Claude follows |
| [EXPLAIN.md](EXPLAIN.md) | **the pedagogy method — how complex ideas become 10-year-old-simple (the core value)** |
| [characters.md](characters.md) | reusable SVG for the stars, Neila & Pip |
| [cast.md](cast.md) | the alien forge + 100+ named guest roster |
| [QUALITY.md](QUALITY.md) | the world-class rubric every *render* is held to |

## Contributing

Ideas welcome — new cast members (name + recipe + "best for"), quality-bar improvements, or new input types. Open an issue or PR.

## License

[MIT](LICENSE) © Alay Merchant
