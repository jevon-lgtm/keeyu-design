---
name: keeyu-design
description: "The Keeyu design system, and the build system that renders it: customer-facing sales collateral in Figma as A4 print documents, the HTML templates behind every customer PDF, and the 1920x1080 decks. Covers What We Heard, Tech Integration Brief, ROI Breakdown, The Offer, Business Case, CS Pre-Scoping Handover and the rest of the Keeyu Golden Set. Use whenever the user asks for a Keeyu document, deck, debrief, brief, one-pager, summary, register or deal artefact, asks what the Keeyu colours, type ramp, gradient or grid are, or references any Keeyu customer deal by name. Also trigger on 'make this in the Keeyu style', 'Keeyu doc', 'on brand for Keeyu', 'discovery debrief', 'pain points doc'. This skill is a strict specification: the values in it are measured from the approved reference and are not to be reinterpreted."
---

# Keeyu Design

Build Keeyu's customer-facing documents. This skill encodes the approved Keeyu
document system exactly as measured from the signed-off reference. It is a
**specification, not inspiration**. Every number in `references/design-tokens.md`
is a measured value. Do not round it, scale it, "improve" it, or substitute a
similar-looking value.

Read sections 1 to 3 every time. They are the generative model: they tell you
what to do in the cases the spec does not enumerate. Sections 4 onward are the
enforcement layer.

---

## 1. Atmosphere

Keeyu documents are **print, not interface**. The reference point is an annual
report or a well-set essay, not a SaaS dashboard. A Keeyu artefact is an argument
made to a customer, and the design exists to make that argument legible in one
pass: the reader should be able to see the shape of the claim before reading a
word of it.

The ground is a near-white `#FAFAFA`, never pure white, carrying a dot grid of
black at 8 percent that measures 255 at the top of the page and 243 at the foot.
It is meant to be barely there. Onto that ground sits a two-family type system
doing all the structural work: **Roboto Serif Light** at display sizes, from 72
down to 19.4, and **Geist** for everything operational. The serif says *this is
the considered claim*; the sans says *this is the detail that supports it*. There
is one weight of the serif and there are no boxes around prose. Hierarchy is
carried by size in a single voice, which is why the ramp is not negotiable.

Colour is almost absent. Five greys carry every level of emphasis from `ink`
`#000000` down to `muted` `#9AA0A6`, and the only chromatic colours in the system
are a semantic pair: **coral means open or a problem, teal means resolved or
confirmed**. Neither is ever decorative, neither is ever reversed. The brand
gradient exists, but it is emitted as *light* rather than painted as fill: a
blurred wash across the top of page one, a rising glow at the foot of every page
after it, a one-pixel border around a table. It never sits flat behind content.

Where the system does become physical, it becomes fully physical. A coloured bar
is not a rectangle with a gradient on it: it has a lit top edge, a body that
falls off in tone, and a coloured glow it casts onto the paper beneath. The hero
wash is not painted on: it is a blurred field of colour that dissolves into the
paper before it reaches the type. The restraint everywhere else is what earns
these moments. A flat coloured rectangle in a Keeyu document reads as an unfinished
version of something, because in this system it is.

---

## 2. Quick reference

If you read nothing else, these are the values that carry the system. Full
tables and provenance are in `references/design-tokens.md`, which is the source
of truth; this block is a convenience.

```
Paper                #FAFAFA        (never #FFFFFF)
Dot grid             #000000 @ 8%, radius 1.5, pitch 20, on every page

Type, display        Roboto Serif Light  72 / 40 / 34 / 32 / 19.4
Type, operational    Geist  19 / 17 / 15 / 14 / 13
Weights              Roboto Serif: Light only.  Geist: Regular and Medium only
Tracking             -0.2% almost everywhere, -1% on stat numerals

Ink                  #000000    display type
Strong               #1A1A1A    the Keeyu-response column, card titles
Body                 #4D5454    intro, meta, closing prose
Soft                 #797E82    the what-we-heard column
Muted                #9AA0A6    labels, captions, footer
Hair                 #ECECEC    every rule and separator (a LINE node)
Rule                 #E0E0E0    the header divider only

Coral                #F6816A  from #FCA694    open, outstanding, a problem
Teal                 #3FA7B7  from #5FBEC8    resolved, confirmed, answered
Brand gradient       #D8F6FF .10 · #9CDFF3 .20 · #FCE1DA .60 · #FF5331 1.0

Radius               6 chip · 10 bar and system card · 12 vertical bar and
                     metric card · 22 well and gradient border box
Well                 #F9F9F9 fill, #ECECEC 1px, radius 22, 1072 wide, 44 pad

A4 page              1240 x 1754, margin 84, content 1072, footer y 1696
Deck                 1920 x 1080, margin 120, content 1680, footer y 1022
Deck type ramp       1.35x the A4 ramp; slide title 54, cover only 96
Hero glow            page 1 at (-100, -329) · every page after at (-100, 1506)
Figma to HTML        scale 0.6403, authored at Figma native size
```

---

## 3. The eight techniques

Each of these has a name because naming it makes it checkable. Where a technique
maps to a non-negotiable in section 4, the number is given.

### 1. The display ramp
72 → 40 → 34 → 32 → 15, one serif at one weight. Hierarchy comes from size
alone: not from boxes, not from weight, not from colour, not from rules. This is
why the ramp cannot be flattened to fit content on a page and why a page that is
running long breaks instead of shrinking. Every body block is one of exactly two
shapes, the two-column comparison row or the single-column prose section block.
*(Non-negotiable 3.)*

### 2. Light, not fill
The brand gradient appears in exactly three forms: a blurred hero wash, a rising
continuation glow, and a 1 px gradient border on a table. It is never a flat
background behind prose, never a tinted panel, never a coloured header band. The
reason is contrast: the moment the gradient becomes a fill, text sits on top of
it and the document stops being print. Light passes behind content; fill
competes with it. *(Non-negotiable 12 and the gradient border box.)*

### 3. The skeuomorphic triad
Every coloured graphic object carries all three layers, always together:

```
gradient body        light stop to base stop
white inner shadow   #FFFFFF @ 0.40-0.45, offset y1, radius 0    the lit edge
coloured drop shadow the object's OWN base colour @ 0.55-0.60    the cast glow
```

Two of the three is not a reduced version of the effect, it is a different and
wrong effect. The inner shadow is what makes the object look lit from above; the
drop shadow in the object's own hue is what makes it look like it is sitting on
paper rather than printed into it. A flat rectangle with a gradient is not
acceptable output. Exact per-object values in `references/design-tokens.md`.
*(Non-negotiable 5.)*

### 4. The semantic dyad
Coral is open, outstanding, a problem, the situation as the customer described
it. Teal is resolved, confirmed, answered, the Keeyu response. That mapping is
fixed. Colour in a Keeyu document is data; it is never decoration and it is never
applied to prose. Everything that is not one of those two states is grey, and the
five-step grey ramp carries all remaining hierarchy. If you need a third state,
it is grey `#B4B8BD → #9AA0A6`, informational. Do not introduce a fourth hue.
*(Non-negotiable 7.)*

### 5. The hero wash is one smooth field
The hero is a single blurred colour gradient inside a clipping frame, and it
holds exactly one child. Nothing is laid over the colour. Its vertical white
profile is what confines the wash to a band and keeps it clear of the type:
full strength at the head of page 1, a pale rise at the foot of every page
after. A hero carrying a second layer is wrong, and the fix is to delete that
layer rather than to tune it.

### 6. A line is a LINE
Every rule, divider and row separator is `figma.createLine()` with a 1 px `hair`
stroke, placed in the auto-layout flow as its own child. Not a 1 px rectangle,
not a frame with three of four stroke edges zeroed. A frame edge is a box
pretending to be a line and cannot be selected or nudged without touching the
container; a rectangle is a shape pretending to be a line and carries a fill
instead of a stroke, so it will not answer to stroke weight, dash or cap. There
are no exemptions: a single-edge stroke anywhere is a defect.
*(Non-negotiable 9.)*

### 7. Prose is never in a box, a token always is
No prose sits in a card, a well, a pill or a tinted panel. The only rounded
containers in the system are the graphic well and the cards inside it. The
inverse is equally strict: a status, a track name, a milestone term or a list
numeral is always a **chip**, never plain text. The chip is the one place a short
label is allowed inside a container, because it is a token rather than prose.
Alongside it sit the gradient border box for tables, the tile grid for category
lists, and the two-column numbered list. A status set as bare text or a run-on
list of categories is a regression, not a neutral choice.
*(Non-negotiables 4 and 14.)*

### 8. Extract, never eyeball
When reproducing a Figma graphic anywhere outside Figma, pull it with
`get_design_context` and transcribe the returned geometry unchanged. Author at
Figma native size and scale the whole module by 0.6403. Approximating a graphic
from a screenshot has been rejected every time it has been tried, because the
skeuomorphic triad does not survive estimation: the offsets are small enough that
guessing them produces something that looks nearly right and reads as cheap.
*(Non-negotiable 10.)*

---

## 4. Non-negotiables

The enforcement layer. Each one records a real rejected attempt, which is why
they are phrased as prohibitions rather than principles. Section 3 tells you what
to build; this tells you what has repeatedly been built instead.

1. **No micro-labels.** No tiny uppercase letter-spaced kickers. No `01`,
   no `/path-style` slugs, no `SECTION 02`, no `TODAY` / `WITH KEEYU` caps
   headers, no axis ticks, no `CLIENT:` chrome. If a label is under 13px or set
   in caps with tracking, delete it. The only caps in the entire document is the
   `KEEYU` wordmark, which is a logo asset.
2. **No em dashes.** Anywhere. Not in prose, not in layer names. Use commas,
   full stops, colons, or the middle dot `·`. This is a hard Keeyu brand rule.
3. **Type hierarchy carries the document, not boxes.** Display 72 → section 40 →
   headline 34 or 32 → body 15. That ramp is the design. Do not flatten it.
   Every body block is one of exactly two shapes, the two-column comparison row
   or the single-column prose section block. See `references/components.md`.
4. **Containers are for graphics only.** Prose never sits in a card, a well, a
   pill, or a tinted box. The only rounded container in the document is the
   graphic well (radius 22) and the cards *inside* it.
5. **Every graphic is skeuomorphic.** Gradient fill + white inner-shadow
   highlight + coloured drop-shadow glow. A flat rectangle is not acceptable.
   The exact recipe is in `references/components.md`.
6. **Copy is verbatim.** When the user supplies source content, reproduce the
   sentences exactly. Reformat and re-lay-out freely; do not rewrite, summarise,
   merge or "tighten" the words unless explicitly asked.
7. **Coral means problem, teal means resolved.** Never decorative, never
   reversed, never applied to prose.
8. **Do not add what the source does not have.** No meta line if the source has
   no meta line. No customer name on an artefact that is written generically. No
   invented headline to cover two source sections you felt like merging. If you
   find yourself writing a line of copy that is not in the source and is not a
   graphic caption, stop: it does not belong in the document.
9. **A line is a `LINE` node.** Every rule, divider and row separator in a Keeyu
   document is a real Figma line: `figma.createLine()`, a 1 px stroke in `hair`,
   placed in the auto-layout flow as its own child. Not a 1 px rectangle with a
   fill, and never a frame with a stroke and three of the four sides zeroed
   (`strokeTopWeight` / `strokeBottomWeight` / `strokeLeftWeight` /
   `strokeRightWeight`). A frame edge is a box pretending to be a line: it cannot
   be selected, nudged or deleted without touching the container. A 1 px
   rectangle is a shape pretending to be a line: it carries a fill instead of a
   stroke, so it will not respond to stroke weight, dash or cap, and a designer
   working on it in Figma has to fight it. If the design shows a line, build a
   line.

   Strokes on a frame are only ever legitimate when **all four** edges are
   visible and the frame is genuinely a box: the graphic well and the white
   cards inside it. Nothing else in the system carries a frame stroke.

   There are **no exemptions**. A single-edge stroke anywhere in a Keeyu
   document is a defect.

10. **Graphics are extracted, never eyeballed.** When reproducing a Figma
    graphic anywhere outside Figma, pull it with `get_design_context` and
    transcribe the returned geometry unchanged. Author at Figma native size and
    scale the whole module by 0.6403. Approximating a graphic from a screenshot
    has been rejected every time it has been tried. See
    `references/html-system.md`.

11. **The wordmark is an asset, never type.** The Keeyu logo is
    `assets/keeyu-logo-black.svg` (and `keeyu-logo-white.svg` for dark grounds).
    It is a wordmark plus an eight-point star mark, and it is the only caps in
    the system. Never set `KEEYU` in a typeface to stand in for it, never
    letter-space Helvetica and call it the logo, never redraw the star. Place
    the SVG. In HTML, inline it as a base64 data URI so the render is
    self-contained.

12. **The page ground is #FAFAFA, not white.** The sheet, the hero's ground,
    the hero's white fade and the dot grid scrim all carry it. Cards and
    wells keep their own fills.

13. **Every document page carries the background dot grid, portrait and
    landscape.** It is not decoration and it is not optional: it is the ground
    the documents sit on. The recipe is two stacked falloffs, and getting it
    from one is the mistake that has been made repeatedly. See
    `references/components.md`, "Page dot grid". This supersedes the 2026-08-04
    amendment to brand system 6.3, which confined the grid to recessed wells:
    as of 2026-08-07 it is page-wide on every A4 artefact, and as of 2026-08-16
    on every landscape page too. Landscape uses
    `Texture / Dot Grid Page 1920x1080` at the same native 20-unit pitch.

14. **Use the chip, the gradient border box, the tile grid and the two-column
    numbered list.** They are in `references/components.md` under "Chips, boxes
    and grids", with geometry in `references/design-tokens.md` and ready-made
    helpers in `references/build-guide.md`. A status set as plain text, a table
    with no border, a run-on list of categories, or a numbered list running one
    full-width column are all now regressions, not neutral choices. The rules
    that matter: coral means open or a problem and teal means confirmed or
    resolved, on chips as everywhere else; a chip carries a token and never
    prose; a boxed table must have its columns renarrowed to 984; and every
    grid and list is auto-layout, never absolute x and y.

Several Keeyu artefacts are **generic templates**, identical across every deal
except for one customer-specific list. On those, the customer is never named in
the body, there is no meta line, and there is no date. The file name carries the
customer, the document does not. Check the source before adding a header block.

---

## 5. Workflow

### 1. Get the content first
Ask for, or read, the source document before opening Figma. Most Keeyu artefacts
already exist as a rendered PDF or a markdown source in the deal folder. Extract
the text verbatim (`pdfplumber` for PDFs). Never invent customer facts, numbers,
system names or people.

### 2. Pick the artefact spec
`references/document-structure.md` gives the section order and page break rules
per artefact. Follow it. If the artefact is not listed, use the What We Heard
structure as the base and keep the same block vocabulary.

### 3. Decide where graphics earn their place
A graphic is justified when it makes a claim in the prose legible at a glance:
a comparison, a sequence, a set of parallel items, a before/after quantity.
It is not justified as decoration. Two to five per document. Each one gets a
serif caption above it stating the point in a full sentence.

Pick the module from `references/components.md` that matches the shape of the
claim. Do not invent a new module type unless none fits.

### 4. Build
Follow `references/build-guide.md`. It contains the page shell, the auto-layout
helper functions, and the exact block sequence. Build one page per `use_figma`
call. Read back node heights only from auto-layout frames that have already been
appended, never from a frame you are still filling.

### 5. Verify
Screenshot every page and verify:

- [ ] Every A4 page carries the dot grid, with the scrim as well as the mask
- [ ] No caps micro-labels anywhere
- [ ] No em dashes
- [ ] Prose is not inside any container
- [ ] Every graphic has gradient + inner highlight + coloured glow
- [ ] Every graphic has a serif caption above it
- [ ] Coral = problem, teal = resolved, consistently
- [ ] Content clears the footer at y 1696
- [ ] Copy matches the source verbatim
- [ ] Nothing has been added that the source does not contain: no invented
      headlines, no meta line, no customer name on a generic template
- [ ] Statuses, track names and milestone terms are chips, not plain text, and
      their colour follows coral-open / teal-confirmed
- [ ] Every table sits in the gradient border box, with columns renarrowed to 984
- [ ] Category lists are a tile grid, not a run-on paragraph, and every tile in
      a row is set to `FILL` vertically so the row is flush
- [ ] Numbered lists of five or more run in two 450 columns with chip numerals
- [ ] Every rule and separator is a `LINE` node with a 1 px stroke. Scan the
      built page: zero nodes named `rule` are of type `RECTANGLE`, and no frame
      anywhere has a single-edge stroke. Search the build script for
      `strokeTopWeight`, `strokeBottomWeight`, `strokeLeftWeight`,
      `strokeRightWeight`: there should be no hits at all
- [ ] The hero is a bare wash: exactly one gradient child, with nothing laid
      over the colour
- [ ] Page 1 has the hero glow at (-100, -329) and every page after it has the
      bottom glow at (-100, 1506)
- [ ] The systems graphic is a clone of the approved instance with retyped
      labels, not a rebuild
- [ ] No two consecutive blocks or slides are item-for-item mirrors of each
      other. If they are, they should have been merged into a paired form
- [ ] Every deck slide except the cover and closer carries six or more content
      items, in two columns, with a rule between items and a label, headline and
      body line on each
- [ ] Footers number 1 to n against the real page count, with no gaps
- [ ] Every deck slide sits on the deck grid in `references/design-tokens.md`:
      title at 54 on y 140, a full-width divider under it, columns starting at
      x 120 / 726 / 1332 or x 120 / 1060, and the last element landing between
      y 900 and y 960. Put the built slide beside a Demo Deck slide: if the
      title size, the divider or the column edges differ, it is wrong
- [ ] Where a claim has a shape, it is carried by a graphic module and not by a
      paragraph. Two to five small technical graphics per deck
- [ ] No slide is carrying fewer than six items, and no slide has an empty
      placeholder frame. If an asset is unavailable, the content it carried has
      been transcribed and set in type instead
- [ ] Two lists that answer each other are in the paired-column form with the
      vertical divider, not two unrelated stacks

For HTML templates, additionally:

- [ ] Every graphic carries a comment naming its Figma node id, native size and
      scale factor, and its values came from `get_design_context`
- [ ] The placeholder set is byte-identical to the template it replaces, and no
      `{{ }}` appears inside any comment
- [ ] The PDF was rendered and every page rasterised and looked at: correct page
      count, correct page size, backgrounds present
- [ ] No page ends with more than a quarter page of dead space
- [ ] The wordmark on every page is the SVG asset with its star mark visible,
      not type, and dark grounds use the white variant
- [ ] The hero wash is smooth on page 1 and on every continuation page, with
      no hard-edged saturated band

---

## 6. Building HTML templates instead of Figma pages

Keeyu's customer PDFs are rendered from HTML templates, not exported from
Figma. If the request is a template, a PDF render, or a change to how customer
documents are generated, read `references/html-system.md` in full before
touching anything. It is the complete specification: the 0.6403 scale constant,
the `.fig-scale` pattern, the measured graphic modules, the placeholder
contract the Python renderer depends on, the Chromium print settings including
the counter-intuitive landscape rule, and the known environment limits.

The template mirrors an existing Figma document block for block. Open that
document and screenshot it before writing a line of HTML. A template invented
from a content brief rather than mirrored from Figma has been rejected outright.

`assets/keeyu_base.css` is the stylesheet. Inject it verbatim, do not fork it.
`assets/example_tech_integration_brief.html` is a complete worked example.
`assets/keeyu-logo-black.svg` and `assets/keeyu-logo-white.svg` are the logo.

---

## 7. References

Read `design-language.md` and `design-tokens.md` on every job. Read the others
as the work requires them. They are short and they are the specification.

- `references/design-language.md` — the language behind the numbers: colour,
  type, depth and space philosophy with the reasoning attached, the derivation
  rules for values the tables do not list, a do/don't pair table, and five
  worked component prompts. Read this before `design-tokens.md` when you are
  making a judgement call rather than looking a value up.

- `references/design-tokens.md` — every measured colour, type, spacing and
  effect value. The source of truth.
- `references/components.md` — build recipes for the page shell, prose blocks,
  and all five graphic modules, with exact geometry.
- `references/document-structure.md` — per-artefact section order, page breaks,
  and the Keeyu Golden Set inventory.
- `references/html-system.md` — the HTML/PDF template system: design-to-code
  extraction, scale constant, graphic modules, placeholder contract, Chromium
  rendering, density rule, and environment limits.
- `references/worked-example.md` — a complete runnable build for one page using
  every component, with the hero and the dot grid built from primitives rather
  than cloned. Read this when there is no existing document to clone from, when
  you are starting a new document family, or when you want the verification
  sweep. It also carries the page-balancing rule.
