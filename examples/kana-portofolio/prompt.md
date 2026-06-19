---
name: twomuch-studio-cluster
description: >
  Generates a single-page WebGL hero artifact in the visual register of a
  maximalist-clinical creative studio homepage: a dense, overlapping cluster
  of heterogeneous 3D primitives (spheres, octagonal prism, gear, capsule)
  rendered with Three.js, floating against a near-white studio backdrop,
  framed by a wordmark that dissolves from solid type into pixel/bitmap type,
  with a pixel-cursor ghost trail and a live running clock in the footer.
  Use this skill to BUILD the artifact (it is the second-pass builder skill;
  it assumes design decisions are already made, not to be re-derived).
---

# Design System

## Colors
- Backdrop: `#F7F7F5` (near-white, slightly warm gray) — the only background
  color on the page. Never use pure `#FFFFFF`.
- Ink/UI text: `#111111` near-black for all typography and cursor outlines.
- Status pill accent: `#FA5708` (orange), used ONLY for the small top-right
  three-dot status pill. This is the single accent color of the chrome layer
  and must not appear elsewhere.
- Object colors (each color belongs to exactly ONE object — do not reuse
  a hue across two different objects):
  - Mustard/amber dome: `#D9A921` base, `#B57B18` shadow side
  - Teal accent stripe (on the amber sphere): `#16514D`
  - Brick-red speckled sphere: base `#B15C5F` blended with white speckle
    noise (simulate via fragment noise, NOT a flat gradient — this sphere
    must read as grainy/glittery, not smooth)
  - Mustard-yellow flat panel (rounded square with embossed spiral/swirl
    relief): `#D9A921`, slightly more saturated than the dome
  - Electric blue sphere: `#51A1FF` base with soft white rim-light falloff
  - Holographic/iridescent capsule: animated or multi-stop gradient cycling
    through magenta `#A23E73`, teal `#3E7A7D`, mustard `#A2841E`, blue
    `#3E5BA2` in soft diagonal bands (simulate oil-slick/holographic foil)
  - Octagonal prism (the structural "frame" object): flat neutral gray-white
    `#E4E4E2` on all faces, NOT colored — its job is structural, not chromatic
  - Gear/sprocket and small white sphere: same neutral white-gray `#EDEDED`
    as the prism, reinforcing they're "uncolored" structural props
  - Bowling-pin-like black object: near-black `#1A1A1A` matte
- Print/sticker objects (the pill strip and rectangular tags wrapped onto
  cylindrical objects) use full-color photographic or UI-screenshot textures
  — these are the only "busy" flat textures and must look like printed
  paper/vinyl wrapped around a 3D surface, complete with a visible fold/crease
  where the texture wraps the curve.

## Typography
- Solid display face: a wide, low-contrast grotesk (e.g. "Neue Montreal",
  "Suisse Int'l", or system fallback `Helvetica Neue`/`Arial Black` at
  tracking -1%). Used for the left ~60% of the wordmark and any "fully
  rendered" UI text (footer label "Featured Projects").
- Pixel/bitmap face: a true bitmap-style monospace (e.g. "Press Start 2P",
  or a custom 8x8 pixel font; fallback `ui-monospace` with `image-rendering:
  pixelated` applied to a canvas-rendered version). Used for the right ~40%
  of the wordmark (the ".STUDIO" portion), the live clock, and both cursor
  sprites.
- No third typeface. Body copy, if any, inherits the solid grotesk at small
  size.

## Spacing & Structure
- Full-bleed canvas (100vw x 100vh), no max-width container.
- Wordmark sits in a fixed top band, ~64–80px tall, with comfortable side
  padding (~24px). It does NOT scale with the 3D scene below it; the 3D
  cluster scales/repositions independently inside the viewport.
- Footer band fixed to the bottom ~32–40px: left-aligned text label
  ("Featured Projects" style copy), right-aligned monospace clock. Both at
  the same baseline.
- The status pill (small rounded-rect with three dots) sits top-right,
  vertically centered with the wordmark's cap-height.

# Section-by-Section Brief

## Section 1 — Hero (the entire viewport)
This is a one-section page for the purposes of this brief (a hero/landing
moment, not a scrolling multi-section site, unless the user asks to extend
it).

**Content**:
- Wordmark "TWOMUCH.STUDIO" top-left, large, full-width-ish
- Status pill (3 dots) top-right
- Dense 3D object cluster centered in the lower 70% of viewport, overlapping
  behind/around the wordmark slightly at its top edge
- Footer-left: small label text, e.g. "Featured Projects"
- Footer-right: live clock, format `HH:MM:SS`

**Composition**: The 3D cluster is NOT centered as a clean composition — it
is deliberately a "dropped pile," with objects at varied depths (some
objects' near edges crossing in front of others), asymmetric weight slightly
left-of-center, and at least 2 objects' silhouettes bleeding off the visible
cluster boundary (e.g. the dark pin-like object exits toward the top edge).
Do not arrange objects in a clean ring or grid — overlap and irregular
spacing is the point.

**Generative element**: None beyond the 3D scene itself and the dissolve
shader (see Signature Element below).

**Typographic treatment**: Wordmark baseline aligns across both type styles
even though the letterforms differ — "TWOMUCH" and ".STUDIO" must sit on
the same visual baseline, same cap-height, so the dissolve reads as one
continuous word breaking apart, not two separate labels.

# Signature Element Spec — The Dissolve

**What it looks like at rest**: The wordmark's left portion ("TWOMUCH") is
fully solid black vector type. Moving rightward across ".STUDIO", individual
letterforms are increasingly represented as a coarse pixel grid (visible
square blocks tracing the letter outline, like a low-res bitmap font),
until the final characters are almost entirely pixel-blocks with gaps,
as if the word is being digitized / dematerializing into data as it's read
left to right.

**What triggers it**: This is a static compositional choice, always present
— it is NOT a hover or scroll trigger by default. (If the user wants it
interactive, an acceptable extension is: hovering near the wordmark
increases pixelation further toward full dissolution, reverting on
mouse-leave — but this is optional, not required.)

**The feeling it should produce**: An uncanny sense that you're watching
text fail to fully render — like catching a system mid-process, equal
parts glitch and craft, never accidental-looking.

# Functional Spec Per Interactive Element

```
[3D Object Cluster — Parallax Tilt]
─────────────────────────────────────────────
State:    cursorX, cursorY: float, normalized -1..1 (0,0 = viewport center)
          clusterGroup.rotation: {x: float, y: float} (radians)

Trigger:  mousemove on window → cursorX = (e.clientX / innerWidth) * 2 - 1
                                  cursorY = (e.clientY / innerHeight) * 2 - 1

Reaction: clusterGroup (the THREE.Group containing all objects) →
          target rotation.y = cursorX * 0.14 rad (~8°)
          target rotation.x = cursorY * 0.10 rad (~6°)
          actual rotation lerps toward target by 0.05 per frame (never snaps)

Pseudocode:
  on mousemove: store normalized cursorX, cursorY
  every frame:
    targetRotY = cursorX * MAX_TILT_Y
    targetRotX = cursorY * MAX_TILT_X
    cluster.rotation.y += (targetRotY - cluster.rotation.y) * 0.05
    cluster.rotation.x += (targetRotX - cluster.rotation.x) * 0.05
```

```
[3D Object Cluster — Idle Drift]
─────────────────────────────────────────────
State:    idleAngle: float, radians, increments every frame

Trigger:  requestAnimationFrame loop, runs from mount, no user input needed

Reaction: clusterGroup → additional rotation.y += 0.0015 per frame,
          stacked ON TOP of (added to, not replacing) the parallax tilt
          rotation, so the cluster always drifts even if the mouse is idle

Pseudocode:
  every frame:
    idleAngle += 0.0015
    cluster.rotation.y = parallaxRotY + idleAngle  // additive, not overwrite
```

```
[Pixel Cursor Ghost Trail]
─────────────────────────────────────────────
State:    trailPoints: array of {x, y, age: int}, max 4 entries

Trigger:  mousemove → unshift {x: e.clientX, y: e.clientY, age: 0} into
          trailPoints; every frame, age += 1 for all entries; remove any
          entry where age > 12; cap array length at 4 (drop oldest)

Reaction: For each entry in trailPoints (oldest to newest) → render one
          pixel-arrow cursor sprite (the jagged bitmap arrow shape) at
          {x, y}, with opacity = 1 - (age / 12), and slightly smaller
          scale for older entries (scale = 1 - age * 0.03)

Pseudocode:
  on mousemove: trailPoints.unshift({x, y, age: 0}); trim to 4
  every frame:
    for each point in trailPoints: point.age += 1
    remove points where age > 12
    for each point: draw pixel-cursor at (point.x, point.y)
                    with opacity (1 - age/12) and scale (1 - age*0.03)
```
[Live Digital Clock]

─────────────────────────────────────────────

State:    currentTime: string "HH:MM:SS"
Trigger:  setInterval(1000ms) → currentTime = formatNow()
Reaction: Footer-right text node → textContent replaced with new

currentTime string, monospace pixel font, no fade/transition

(hard cut every second, reinforcing "system clock" honesty)
Pseudocode:

every 1000ms:

now = new Date()

currentTime = pad(now.hours) + ":" + pad(now.minutes) + ":" + pad(now.seconds)

footerClockElement.textContent = currentTime

# Animation and Interaction Rules

These things animate: the object cluster (parallax tilt + idle drift,
continuous), the cursor ghost trail (follows real cursor, continuous while
moving), the live clock (ticks every second). Nothing else moves. The
wordmark dissolve effect is a static render, not an animation, unless
explicitly extended to hover-react per the Signature Element spec. No
page-load entrance animations, no scroll-triggered reveals, no button hover
states beyond the optional wordmark hover — this page does not behave like
a marketing site with micro-interactions on every element.

# Anti-Patterns for This Brief

- Do NOT smooth the brick-red sphere into a clean gradient — it must keep
  its grainy/speckled noise texture, or it will read as generic 3D-render
  instead of "studio object with character."
- Do NOT center or grid-align the object cluster — any composition that
  looks balanced/symmetric betrays the "dropped pile" mood and will read as
  a SaaS product-shot, which this brief explicitly rejects.
- Do NOT round every corner or add soft shadows uniformly — the structural
  gray objects (prism, gear) should stay flat/matte and slightly stark; over-
  softening the whole scene flattens the tension between "precise" and
  "cluttered."
- Do NOT animate the wordmark dissolve as a looping/repeating effect (e.g.
  constantly cycling pixelation back and forth) — it should read as a fixed
  state of being, not a gimmick loop, or it stops feeling like an aesthetic
  choice and starts feeling like a loading spinner.
- Do NOT add color accents beyond the single orange status pill in the UI
  chrome layer (wordmark, footer, pill) — introducing a second chrome accent
  color dilutes the rule that color belongs exclusively to the 3D objects.

# Implementation Notes (honesty about source ambiguity)

This skill was derived from a single static screenshot. The interactive
behaviors above (parallax tilt, idle drift, cursor trail, live clock) are
**informed inferences** based on visual cues in the image (a ghost-trailed
cursor sprite, a running clock readout) — they are not confirmed behaviors
of an original live site, because no live site was observed. Build them as
sensible defaults for "a creative studio cluster," and treat them as freely
adjustable rather than as ground truth to preserve exactly.