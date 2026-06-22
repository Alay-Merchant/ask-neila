# Neila & Pip — reusable SVG

Paste these `<g>` groups into the SVG. Move them with the wrapping `transform="translate(x,y)"`.
Scale by wrapping in `transform="translate(x,y) scale(s)"`. Swap the marked bits to change expression.
Keep the colors — that's what makes them recognizable.

## Neila (host alien)

Teal body, three eyes, two antennae, friendly. ~120×140 at scale 1.

```svg
<g id="neila" transform="translate(0,0)">
  <!-- antennae -->
  <line x1="48" y1="20" x2="40" y2="2" stroke="#2A8C80" stroke-width="5" stroke-linecap="round"/>
  <line x1="72" y1="20" x2="80" y2="2" stroke="#2A8C80" stroke-width="5" stroke-linecap="round"/>
  <circle cx="38" cy="0" r="6" fill="#FFD23F"/>
  <circle cx="82" cy="0" r="6" fill="#FFD23F"/>
  <!-- body -->
  <ellipse cx="60" cy="75" rx="52" ry="58" fill="#3FBFB0" stroke="#2A8C80" stroke-width="4"/>
  <!-- arms (the right one points; raise/lower y to gesture) -->
  <path d="M14 80 Q-4 78 -10 64" stroke="#2A8C80" stroke-width="6" fill="none" stroke-linecap="round"/>
  <path d="M106 80 Q126 76 134 60" stroke="#2A8C80" stroke-width="6" fill="none" stroke-linecap="round"/>
  <circle cx="-12" cy="62" r="6" fill="#3FBFB0" stroke="#2A8C80" stroke-width="3"/>
  <circle cx="136" cy="58" r="6" fill="#3FBFB0" stroke="#2A8C80" stroke-width="3"/>
  <!-- three eyes -->
  <g id="neila-eyes">
    <circle cx="38" cy="62" r="11" fill="#fff" stroke="#2A8C80" stroke-width="3"/>
    <circle cx="60" cy="58" r="11" fill="#fff" stroke="#2A8C80" stroke-width="3"/>
    <circle cx="82" cy="62" r="11" fill="#fff" stroke="#2A8C80" stroke-width="3"/>
    <circle cx="38" cy="63" r="4.5" fill="#1A1A2E"/>
    <circle cx="60" cy="59" r="4.5" fill="#1A1A2E"/>
    <circle cx="82" cy="63" r="4.5" fill="#1A1A2E"/>
    <!-- blink: optional, drop on each eye white -->
    <!-- <animate attributeName="ry" values="11;1;11" dur="0.3s" begin="3s;7s" repeatCount="indefinite"/> -->
  </g>
  <!-- mouth: this is a happy smile. Swap d for other moods (see below) -->
  <path id="neila-mouth" d="M44 92 Q60 108 76 92" stroke="#1A1A2E" stroke-width="4" fill="none" stroke-linecap="round"/>
  <!-- cheeks -->
  <circle cx="30" cy="86" r="6" fill="#FF8FB1" opacity="0.6"/>
  <circle cx="90" cy="86" r="6" fill="#FF8FB1" opacity="0.6"/>
</g>
```

**Neila mouth swaps** (replace the `d` on `#neila-mouth`):
- smile: `M44 92 Q60 108 76 92`
- talking (open): use `<ellipse cx="60" cy="96" rx="9" ry="7" fill="#1A1A2E"/>` instead of the path
- excited grin: `M42 90 Q60 112 78 90` + add `<path d="M42 90 H78" stroke="#1A1A2E" stroke-width="3"/>`

## Pip (Neila's alien dog)

Lavender, one big eye, two floppy antenna-ears, tail, four legs. ~90×80 at scale 1.

```svg
<g id="pip" transform="translate(0,0)">
  <!-- floppy antenna-ears -->
  <path d="M26 24 Q10 10 4 26" stroke="#9B7FD4" stroke-width="6" fill="none" stroke-linecap="round"/>
  <path d="M58 24 Q74 10 80 26" stroke="#9B7FD4" stroke-width="6" fill="none" stroke-linecap="round"/>
  <circle cx="4" cy="27" r="5" fill="#FFD23F"/>
  <circle cx="80" cy="27" r="5" fill="#FFD23F"/>
  <!-- body -->
  <ellipse cx="42" cy="48" rx="36" ry="30" fill="#B59FE6" stroke="#9B7FD4" stroke-width="4"/>
  <!-- legs -->
  <rect x="18" y="70" width="8" height="12" rx="4" fill="#9B7FD4"/>
  <rect x="32" y="72" width="8" height="12" rx="4" fill="#9B7FD4"/>
  <rect x="46" y="72" width="8" height="12" rx="4" fill="#9B7FD4"/>
  <rect x="60" y="70" width="8" height="12" rx="4" fill="#9B7FD4"/>
  <!-- tail (wiggle by animating transform rotate) -->
  <path id="pip-tail" d="M78 50 Q92 44 90 32" stroke="#9B7FD4" stroke-width="6" fill="none" stroke-linecap="round"/>
  <!-- one big eye (this is the whole face) -->
  <circle cx="42" cy="44" r="16" fill="#fff" stroke="#9B7FD4" stroke-width="3"/>
  <circle id="pip-pupil" cx="42" cy="46" r="7" fill="#1A1A2E"/>
  <circle cx="46" cy="42" r="2.5" fill="#fff"/>
  <!-- little smile -->
  <path d="M34 64 Q42 72 50 64" stroke="#1A1A2E" stroke-width="3" fill="none" stroke-linecap="round"/>
</g>
```

**Pip mood swaps** (move `#pip-pupil`):
- happy/neutral: pupil at `cx=42 cy=46`
- confused: pupil up-left `cx=38 cy=42`, tilt whole `#pip` group `rotate(-8)`
- amazed: enlarge pupil `r=9`, add `<circle cx="42" cy="44" r="22" fill="none" stroke="#FFD23F" stroke-width="2" opacity="0.7"/>` shock lines

## Speech bubble (reuse for every concept)

```svg
<g transform="translate(0,0)">
  <rect x="0" y="0" width="240" height="90" rx="18" fill="#FFFDF5" stroke="#1A1A2E" stroke-width="3"/>
  <path d="M30 88 L20 112 L52 88 Z" fill="#FFFDF5" stroke="#1A1A2E" stroke-width="3"/>
  <text x="120" y="36" font-family="'Fredoka','Comic Sans MS',sans-serif" font-size="16"
        font-weight="600" fill="#1A1A2E" text-anchor="middle">
    <tspan x="120" dy="0">Concept name</tspan>
    <tspan x="120" dy="24" font-size="14" font-weight="400">plain one-liner here</tspan>
  </text>
</g>
```

## Palette

| use | hex |
|-----|-----|
| Neila body | `#3FBFB0` / outline `#2A8C80` |
| Pip body | `#B59FE6` / outline `#9B7FD4` |
| antennae tips | `#FFD23F` |
| cheeks/accent pink | `#FF8FB1` |
| ink (outlines/text) | `#1A1A2E` |
| bubble paper | `#FFFDF5` |
| backgrounds | warm pastels: `#FFF3D6`, `#D6F0FF`, `#FFE0EC`, `#E4FFD6` |

Guest aliens: pick any bright hue NOT teal/lavender so they read as "guests", same thick-outline rounded style.
