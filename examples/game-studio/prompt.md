---
name: archival-tech-editorial
description: >
  Use this skill to build a single-page or multi-section editorial layout that tells a
  biographical or historical story about a tech/design figure, in the visual register of
  an archived early-computer document. Triggers: "make it feel like an old Macintosh
  document", "retro tech biography page", "editorial layout with pixel art borders",
  or any brief referencing 1980s personal computing aesthetics, dot-matrix typography,
  or "screenshot inside a page" composition.
---

# Archival Tech Editorial — Generated Skill

## 1. Design System

**Colors (hex)**
- `--ink: #1a1a1a` — all body text, rules, line art strokes. Never lightened for hierarchy; hierarchy comes from size/weight, not color dilution.
- `--paper: #f0ede4` — page background. Slightly warm off-white, never pure white (#fff reads too clinical/SaaS).
- `--accent-yellow: #e8b04b` — highlight marker behind key phrases, secondary pixel-art fills (bags, graphs). Used sparingly — if more than ~10% of a section is yellow, pull back.
- `--accent-blue: #a8c8e8` — reserved exclusively for "this is a computer artifact" signals: window title bars, pixel cloud borders, screenshot chrome. Never used for plain text emphasis — that would blur the rule that blue = digital artifact, black/yellow = editorial content.
- `--checker-grey: #d8d8d8` / `#ffffff` — outer frame checkerboard pattern only.

**Typefaces + roles**
- Display/headline: `IBM Plex Mono, weight 700` (fallback: a true pixel font like "Press Start 2P" only for very short hero phrases, never body). Role: every headline reads like a terminal command or dot-matrix banner — mechanical, no humanist warmth.
- Body/caption: `IBM Plex Mono, weight 400`. Role: every word on the page, including captions and footnotes, comes from the same monospace family — this is non-negotiable, because mixing in a humanist sans for body text breaks the "single typewriter authored this whole document" illusion.
- Import: `@import url('https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:wght@400;500;700&display=swap');`

**Spacing scale**
- Base unit: 8px. Section padding: 48–64px vertical, 40–56px horizontal on desktop; collapses to 24px/16px on mobile.
- Text columns never touch the page edge — minimum 40px gutter from the checkerboard frame at all times.

**Structural rules**
- Outer frame: fixed checkerboard border (16–20px thick) wraps the entire page, simulating a scanned/archived document edge. This frame never disappears, including on mobile.
- Every section is a distinct "card" with a hairline 2px black border — sections stack with a visible seam, never bleed into each other.

## 2. Section-by-Section Brief

**Section 1 — Origin**
- Content: large two-line headline (subject's defining early ambition), birth statement in bold caps, indented narrative paragraphs to the right of small archival-style photos stacked in the left column.
- Composition: pixel-cloud strip runs along the top edge in `--accent-blue`; headline sits left-aligned below it with generous top air; body splits into a left rail (photos, ~20% width) and a right rail (narrative text, ~80% width, itself indented in stepped paragraph blocks moving rightward to suggest a timeline).
- Generative art: none — this section uses no canvas/procedural element; the only artwork is a static pixel-art illustration (e.g. a bag/object icon) anchored top-right, hand-drawn at a fixed pixel grid, not algorithmically generated.
- Typographic treatment: the birth-fact sentence is set in bold caps at body size to act as a structural anchor between headline and narrative — it is not a sub-headline, it is a fact-stamp.

**Section 2 — Turning point / the call**
- Content: a quote-style headline in large caps (the moment of change, often literally quoted), narrative text describing the circumstance, and a "screenshot" component showing a dialog/chat bubble.
- Composition: a window-chrome bar (title text centered, in `--accent-blue` fill) sits as the seam between Section 1 and Section 2, visually behaving like a real OS window header sitting on top of the page. Below it, a small pixel-art creature/object sits left, a speech-bubble dialog box sits center-left containing a first-person quote, and a cluster of pixel bar-chart icons sits bottom-right.
- Generative art: none — bar-chart icons and creature are static pixel-art assets, hand-placed.
- Typographic treatment: the first-person quote inside the dialog bubble uses the same mono body font but is visually boxed (1px black border, white fill, small drop-corner notch) to read as a literal screen element, not as a pull-quote.

## 3. Signature Element Spec

**The element**: The window-chrome divider — a horizontal bar styled exactly like a classic OS title bar (centered bold label, flanked by thin border, sitting in `--accent-blue` or white-on-black), placed at the seam between every two major sections instead of a plain horizontal rule.

- At rest: it sits flush across the full content width, distinct from the paper-colored sections above and below it — it should look like a separate "window" was screenshotted and dropped into the page.
- Trigger: none — it is a static compositional device, always present, not user- or time-triggered.
- Feeling: the reader should feel a small jolt of recognition — "oh, this is mimicking software" — exactly once per section break, never so often it becomes decorative wallpaper.

## 4. Functional Spec per Interactive Element

None. Per Pass 1, this brief has no user interaction — the page is a static archival read. Do not add hover states, scroll-triggered counters, clickable elements, or cursor effects; doing so would contradict the "arsip" mood and the explicit no-interaction brief.

(If a future revision of this brief introduces interaction — e.g. a draggable timeline — this section must be rewritten with full State/Trigger/Reaction blocks before building.)

## 5. Animation and Interaction Rules

- Nothing animates continuously. No looping motion, no parallax, no cursor-follow effects.
- The only permitted motion is a single, slow opacity/translateY fade-in (300–400ms, ease-out) as each section enters the viewport on scroll — this mimics a document "rendering in," not a marketing reveal.
- No hover states on photos, icons, or dialog boxes. They are archival images, not buttons — adding hover affordances would falsely imply interactivity.
- Everything else is static. If in doubt about whether something should move, the default answer is no.

## 6. Anti-Patterns for This Brief

- Do not use rounded corners, drop shadows, or gradients anywhere — these read as modern SaaS polish and directly contradict "must not feel like a SaaS landing page."
- Do not introduce a second non-monospace typeface "for variety" — variety here comes from weight and size within one family, not from font mixing.
- Do not make the pixel-art illustrations cute, bouncy, or cartoonish in proportion — they must stay flat, blocky, and deliberately crude, like genuine 1-bit/8-bit era art, not a polished "retro-style" illustration commissioned today.
- Do not let `--accent-blue` leak into plain text or buttons — it is reserved strictly for signaling "this is a computer/software artifact," and using it elsewhere dilutes that signal.
- Do not add transitions, hover animations, or interactive polish anywhere — this brief is explicitly non-interactive, and over-animating it would betray the archival mood.