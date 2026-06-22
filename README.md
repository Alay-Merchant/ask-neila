# 🛸 ask-neila

> Turn any paragraph, file, PDF, or PowerPoint into a colorful illustrated explainer — where friendly alien characters break down the hard concepts in dead-simple language.

**ask-neila** is a [Claude Code](https://claude.com/claude-code) skill. Point it at some text and it pulls out the few ideas that actually matter, rewrites each in plain words with a concrete analogy, and draws a single picture you can download — starring **Neila** the alien and her alien dog **Pip**, plus a cast of 100+ topic-themed guests.

The real value is the *simplification*. The aliens are the wrapper that makes it stick.

## What it does

```
/ask-neila <paste a paragraph here>      # explain pasted text
/ask-neila path/to/lecture.pdf           # explain a PDF
/ask-neila path/to/slides.pptx           # explain a PowerPoint
/ask-neila path/to/notes.md              # explain a markdown/text file
```

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
| [characters.md](characters.md) | reusable SVG for the stars, Neila & Pip |
| [cast.md](cast.md) | the alien forge + 100+ named guest roster |
| [QUALITY.md](QUALITY.md) | the world-class rubric every render is held to |

## Contributing

Ideas welcome — new cast members (name + recipe + "best for"), quality-bar improvements, or new input types. Open an issue or PR.

## License

[MIT](LICENSE) © Alay Merchant
