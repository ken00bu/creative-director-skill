---
name: orbital-portfolio-builder
description: >
  Generates a single-page creative studio portfolio where dozens of photo
  cards are arranged on the surface of a 3D sphere using spherical point
  distribution, rendered via Canvas/WebGL with real-time rotation driven by
  cursor movement or autonomous time-based rotation. Clinical, monospace,
  black-and-white UI with the photo cards themselves as the only color source.
---

# Orbital Portfolio Builder

## 1. Design System

**Colors**
- Background: `#FFFFFF` (pure white, zero off-white tint)
- Primary text/UI: `#0A0A0A` (near-black, not pure #000 to avoid harsh contrast)
- Button border: `#0A0A0A`, 1px solid
- Button background: transparent, white on hover-invert optional but NOT required
- Photo cards: full native color of each image, completely uncontrolled — this is the
  only place color exists on the page

**Typography**
- Single typeface: `IBM Plex Mono` or `JetBrains Mono` (import via Google Fonts or
  self-hosted woff2)
- Header title ("CREATIVE STUDIO"): 11px, weight 500, letter-spacing 0.15em, uppercase
- Navigation links (footer): 11px, weight 400, letter-spacing 0.05em, uppercase
- Copyright/legal line: 8px, weight 400, letter-spacing 0.02em, opacity 0.6
- No second typeface anywhere. No serif, no display font, no body copy font.

**Spacing scale**
- Header sits 24px from top edge, horizontally centered
- Footer button row sits 24px from bottom edge, horizontally centered
- Sphere occupies the full remaining vertical space, vertically centered between
  header and footer
- Button padding: 8px vertical, 16px horizontal
- Gap between footer buttons: 8px

**Structural rules**
- No border-radius greater than 2px anywhere except button corners (sharp, near-zero)
- No drop shadows, no gradients, no glassmorphism
- No background color blocks — everything floats on pure white

## 2. Section-by-Section Brief

### Header
- Content: "CREATIVE STUDIO" (placeholder — replace with actual studio name)
- Composition: single line, horizontally centered, locked to top of viewport
- No generative art here
- Typographic treatment: smallest text on the page relative to its prominence —
  prominence comes from position and isolation, not size

### Sphere (main content)
- Content: 50–80 photo/video thumbnail cards, each a rotated rectangle (mix of
  portrait and landscape aspect ratios, slightly varied sizes)
- Composition: cards distributed across a spherical surface using Fibonacci sphere
  distribution (golden angle method) so spacing is even with no clustering or gaps
- Generative art: YES — the sphere itself is the generative system. Each card's
  position on the sphere is computed once at load (fixed base coordinates), then
  rotated live based on global rotationX/rotationY. Cards do not move independently
  of the sphere's rotation.
- Typographic treatment: none — this section contains zero text

### Footer navigation
- Content: "HANDS FREE?", "CONTACT", "PHOTOGRAPHY ↳", "SHOP ↳", "INSTAGRAM ↳"
  rendered as individual bordered button/chip elements in a single row
- Composition: row of discrete bordered rectangles, horizontally centered, equal
  vertical padding, gap of 8px between each
- No generative art
- Typographic treatment: identical style across all five buttons — no visual
  hierarchy between them despite different functions

### Legal line (bottom-most)
- Content: "© 2026 [STUDIO NAME] LTD. REGISTERED IN ENGLAND AND WALES. COMPANY NO.
  [PLACEHOLDER]. TERMS & CONDITIONS"
- Composition: single line, centered, smallest text on page, reduced opacity
- No generative art

## 3. Signature Element Spec

**What it is**: The rotating sphere of photo cards.

**At rest**: When `isHandsFree` is true, the sphere rotates continuously and slowly
on its Y axis (and a subtle secondary drift on X) — cards drift past the viewer like
a slow-orbiting satellite field, none ever fully facing the camera for long.

**In motion (user-controlled)**: When the user moves the cursor anywhere over the
viewport, the sphere's rotation tracks cursor position — moving the cursor right
spins the sphere to reveal cards on that side; moving up/down tilts the sphere's
vertical axis. The motion has slight easing/lag (not 1:1 instant) so it feels like
it has mass.

**Trigger**: Page load → autonomous rotation begins immediately. Mouse move → takes
over rotation control smoothly (no jump cut). Click "HANDS FREE?" → toggles back to
autonomous mode.

**Feeling it should produce**: The viewer should feel like they are looking at a
specimen under controlled examination — precise, weighty, slightly clinical — like
rotating a 3D-scanned object rather than browsing a casual photo gallery.

## 4. Functional Spec Per Interactive Element
Sphere Rotation Control

─────────────────────────────────────────────

State:    rotationX: float, degrees, range unrestricted (wraps at 360)

rotationY: float, degrees, range unrestricted (wraps at 360)

isHandsFree: boolean, default true on load

autoRotateSpeed: float, default 0.03 deg/frame
Trigger:  Mouse move over viewport (while isHandsFree is false) →

rotationY = map(mouseX, 0, viewportWidth, -30, 30)

rotationX = map(mouseY, 0, viewportHeight, -15, 15)

Click "HANDS FREE?" button →

isHandsFree = !isHandsFree

Page load / no mouse interaction for >2s →

isHandsFree resumes true automatically (optional graceful fallback)
Reaction: Every card →

recalculate 3D position via rotation matrix applied to card's fixed

base spherical coordinate

project to 2D screen x/y using simple perspective projection

(divide by z-depth + camera distance)

Cards on far side of sphere (z < 0) →

opacity interpolated down to 0.35–0.5 based on z-depth

Cards on near side of sphere (z > 0) →

opacity at full 1.0, scale boosted up to 1.1x at the closest point

"HANDS FREE?" button label →

no text change; could optionally show pressed/active visual state

(border weight increases from 1px to 1.5px) when isHandsFree is true
Pseudocode:

// On load: distribute N cards using Fibonacci sphere

for i in 0..N:

theta = acos(1 - 2*(i+0.5)/N)

phi = goldenAngle * i

card[i].basePos = sphericalToCartesian(theta, phi, radius)
// Every frame:

if not isHandsFree: rotationX/Y = mouseInfluence (with easing toward target)

else: rotationY += autoRotateSpeed
for each card:

rotated = applyRotationMatrix(card.basePos, rotationX, rotationY)

screen = projectPerspective(rotated, cameraDistance)

card.style = { x: screen.x, y: screen.y, scale: screen.scale, opacity: depthToOpacity(rotated.z) }

## 5. Animation and Interaction Rules

These things animate: the sphere's rotation (continuous, either autonomous or
cursor-driven) and each card's resulting position/scale/opacity recalculation every
frame. Nothing else moves. The header text, footer buttons, and legal line have zero
transitions, zero hover animations beyond a possible 1px border-weight change on
"HANDS FREE?", and zero entrance animations on load (everything appears instantly
except the sphere, which begins rotating from frame one).

Hover states are minimal: buttons may invert background/text color on hover as the
only hover feedback in the entire page. No other interactive states exist — no
tooltips, no card-level hover effects, no cursor change beyond default/pointer.

## 6. Anti-Patterns for This Brief

- Do NOT add drop shadows or glow effects to the photo cards to make the sphere
  "pop" — this breaks the clinical, flat mood.
- Do NOT introduce a second typeface for the header to make it feel more "branded"
  — the monospace uniformity across header/footer/legal is the point.
- Do NOT add color to any UI chrome (buttons, borders, background) to compensate for
  the otherwise colorless layout — the photo cards must remain the sole color source.
- Do NOT make individual cards independently draggable or clickable with hover
  zoom/lightbox — the sphere moves as one rigid object, not as loose particles.
- Do NOT center the sphere with heavy padding or a contained box/frame — it must
  feel like it floats in unbounded white space, not framed inside a card or section.