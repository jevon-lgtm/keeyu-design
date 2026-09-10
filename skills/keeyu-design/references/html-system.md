# The Keeyu HTML/PDF System

Keeyu's customer PDFs are not exported from Figma. They are rendered from HTML
templates by a Python renderer that substitutes `{{PLACEHOLDER}}` tokens and
prints the page with headless Chromium. Figma is where the document is designed;
these templates are where the design is *reproduced*, pixel for pixel, so that
every customer PDF is the Figma document with the customer's data in it.

The whole point of this reference is that a rendered PDF and its Figma page must
be indistinguishable side by side. Anything less has been rejected.

---

## 1. The one rule that matters

**Do not eyeball a graphic. Extract it.**

Every graphic in a Keeyu template was measured out of Figma with
`get_design_context`, which returns the node as React + Tailwind with exact
geometry, exact gradient stops, exact shadow values. Those numbers go into the
CSS unchanged. Hand-approximating a graphic from a screenshot produces the thing
the client called "pretty fucked" — the proportions drift, the gradient angle is
wrong, the shadow is a guess.

The extraction workflow, in order:

1. Load the Figma design-to-code skill resource first. This is mandatory and the
   call fails or degrades without it:
   `skill://figma/figma-design-to-code/SKILL.md`
2. Call `get_design_context` on the graphic's node id, passing
   `skillNames: "resource:figma-design-to-code"`.
3. Read the returned geometry: width, height, absolute x/y of every child,
   border radius, gradient stops and angle, box-shadow offsets and colours.
4. Transcribe those numbers into a CSS module at **Figma native size**. Do not
   convert them. Do not "adapt them for print".
5. Wrap the module in `.fig-scale` so it lands at the right size on the page
   (section 3 below).

If the node cannot be reached, do not invent it. Flag the graphic and leave the
template with a captioned placeholder that says what it needs.

---

## 2. Page geometry and the scale constant

The Figma canvas is **1240 px wide = 210 mm = one A4 page**.
Chromium prints A4 at 96 dpi = **794 px**.

    Conversion factor: 794 / 1240 = 0.6403

Everything measured in Figma is multiplied by 0.6403 to reach CSS px. Rather
than doing that arithmetic on every value, the page tokens are pre-converted and
the graphics are scaled wholesale by transform.

Tokens, already converted, in `assets/keeyu_base.css`:

    --page-w:       794px      (A4 width at 96 dpi)
    --page-h:       1123px     (A4 height at 96 dpi)
    --margin:       53.8px     (84 in Figma)
    --content-w:    686.4px    (1072 in Figma)
    --col-headline: 284.3px    (444 in Figma)
    --col-response: 329.1px    (514 in Figma)
    --col-gap:      68.5px     (107 in Figma)
    --footer-y:     1086px
    --type-scale:   1

`--type-scale` is the single lever for the whole type ramp. Body text lands
around 7.2 pt at scale 1, which is small for print; if a printed proof reads
tight, raise `--type-scale` and nothing else. Never nudge individual font sizes
to fix a page that is running long — that breaks the ramp, which is the design.

---

## 3. The `.fig-scale` pattern

Author every graphic at its Figma native pixel size, then scale the whole thing
down as one unit. This is why the graphics finally matched: no per-value
rounding error, no drift between the hub and the cards.

```css
.fig-scale        { position: relative; overflow: hidden; }
.fig-scale > .fig { transform: scale(0.6403);
                    transform-origin: top left;
                    position: absolute; top: 0; left: 0; }
```

**A caution learned the hard way, 2026-08-07.** `transform` is a paint-time
operation: the element still lays out at its native width. That is fine for a
graphic module sitting inside a page, which is what this pattern is for. It is
NOT fine for scaling a whole page: Chromium's print path rasterises at the
untransformed width and lands the entire document at two thirds size in the top
left corner of the sheet. When scaling a full page, use `zoom`, which scales
layout, so the used size really is 794 x 1123.

Usage. The outer height is the native height times 0.6403, rounded to the page
rhythm; the inner div carries the untouched native artwork:

```html
<!-- Systems graphic · Figma node 123:61491, native 1072 x 296, scaled 0.6403 -->
<div class="fig-scale" style="height:190px;margin-top:12.8px">
  <div class="fig">
    ... native-size markup ...
  </div>
</div>
```

Always leave that comment: node id, native size, scale factor. It is how the
next person re-extracts the graphic when the Figma page changes.

---

## 4. Measured graphic modules

These are transcribed from `get_design_context` and from reading the nodes
directly with `use_figma`. They are measurements, not suggestions. Reproduce
them exactly.

Start with **4d, the hero wash**. It appears on every page of every artefact
and it is the one thing a reader sees before anything else.

A note on tooling. `get_design_context` flattens a node to its rendered
appearance, so a construction made of many stacked children comes back as one
flat surface with no hint of how it was built. When a surface looks richer in
Figma than the returned code implies, read the node tree with `use_figma`
instead: dump `fills`, `strokes`, `effects`, `blendMode` and `opacity` for the
node and its children.

### 4a. Systems graphic (Figma node 123:61491, native 1072 × 296)

A gradient hub with the Keeyu wordmark, five white system cards below it, and a
dashed connector tree between them.

```css
.sys       { width:1072px; height:296px; position:relative;
             background:#F9F9F9; border:1px solid #ECECEC; border-radius:22px; }

.sys-hub   { position:absolute; left:431px; top:41px; width:208px; height:58px;
             border-radius:12px;
             background:
               linear-gradient(17.04deg, rgba(216,246,255,.65) 4%,
                                         rgba(156,223,243,.65) 22.3%,
                                         rgba(252,225,218,.65) 58.6%,
                                         rgba(255,83,49,.65) 98%),
               linear-gradient(90deg, #E5E5E5, #E5E5E5);
             box-shadow: 0 10px 20px -8px rgba(63,167,183,.55),
                         inset 0 1px 0 0 rgba(255,255,255,.4); }

.sys-hub span { position:absolute; inset:0; display:flex;
                align-items:center; justify-content:center;
                font-family:'Geist',sans-serif; font-weight:500;
                font-size:19px; color:#4D5454; }

.sys-card  { position:absolute; top:151px; width:184px; height:66px;
             background:#fff; border:1px solid #EAEAEA; border-radius:10px;
             box-shadow: 0 1px 1px 0 rgba(0,0,0,.04),
                         0 3px 6px 0 rgba(0,0,0,.05);
             display:flex; align-items:center; justify-content:center;
             font-family:'Geist',sans-serif; font-weight:500;
             font-size:14px; color:#1A1A1A; text-align:center; }

.sys-caption { position:absolute; left:43px; top:231px; width:700px;
               font-family:'Geist',sans-serif; font-weight:400;
               font-size:14px; color:#9AA0A6; }
```

**Card x positions are set inline per card: 43, 243, 443, 643, 843.** Do not
reach for `nth-of-type` to position them. The hub div is a sibling and gets
counted, which silently shifts every card by one slot and puts Carriers first.
This failure has happened and it is not obvious in a thumbnail.

Connector wires, as an SVG at native size sitting inside `.sys`:

```html
<svg class="sys-wires" width="1072" height="296" viewBox="0 0 1072 296" fill="none">
  <g stroke="#CBCBCB" stroke-width="1" stroke-dasharray="4 4" stroke-linecap="round">
    <path d="M135 151 V76 Q135 66 145 66 H925 Q935 66 935 76 V151"/>
    <path d="M335 151 V94 Q335 84 345 84 H725 Q735 84 735 94 V151"/>
    <path d="M535 99 V151"/>
  </g>
</svg>
```

### 4b. The wordmark

The logo is not a graphic to be reproduced. It is a fixed asset that ships with
this skill and must be placed unmodified:

    assets/keeyu-logo-black.svg   viewBox 0 0 131 31, paths fill #262626
    assets/keeyu-logo-white.svg   the same paths, fill #FFFFFF, for dark grounds

It is the wordmark `KEEYU` followed by an eight-point star mark. Both are
outlined paths, not live text, so nothing depends on a font being installed.
Never substitute type for it. A previous render used letter-spaced Helvetica as
a stand-in and shipped a document with no star mark at all.

Inline it as a base64 data URI so the rendered HTML is self-contained:

```python
def _svg_uri(path):
    import base64
    return 'data:image/svg+xml;base64,' + base64.b64encode(open(path,'rb').read()).decode()

LOGO       = _svg_uri('keeyu-logo-black.svg')
LOGO_WHITE = _svg_uri('keeyu-logo-white.svg')
```

The renderer's templates carry the bare tokens `LOGO_BLACK_PATH` and
`LOGO_WHITE_PATH` as `src` values. Substitute each with the matching data URI;
they are different assets and routing both to black loses the logo on any dark
slide. Placement is fixed by `.logo` in the stylesheet: `left: 57px`,
`top: 44.8px`, `width: 83.2px`. Set width only and let the height follow the
131:31 aspect. Never set both.

### 4c. Gradient-border card (the next-step block)

The design is a 1 px gradient border around white. The obvious CSS solution,
`mask` plus `mask-composite: exclude`, **renders as a solid gradient block in
Chromium's print path**. Use padding and an inner div instead:

```css
.next-step         { margin-top: 34.6px; border-radius: 14px; padding: 1px;
                     background: linear-gradient(100deg,
                                 #9CDFF3, #D8F6FF 35%, #FCE1DA 70%, #FF5331); }
.next-step > .inner { background: var(--white); border-radius: 13px;
                      padding: 25.6px 28.8px; }
```

### 4d. The hero wash

This is on every page of every document, so getting it wrong is the most
expensive mistake available. In Figma it is a frame named `hero`, native
1440 × 684, holding two things:

1. `gradient` — a rectangle 1751 × 554 at x -100, opacity 0.8, carrying a
   four-stop linear gradient whose axis runs at 267.76deg, which is 2.2deg off
   horizontal. Coral at the left edge, pale blue past the right edge.
2. A `PROGRESSIVE` layer blur on that rectangle, startRadius 98.8, running top
   to bottom.

The whole hero is placed at (-100, -329) on page 1 and (-100, 1506) on every
following page. On the 1920 × 1080 landscape canvas it is the same module at
exactly 1.5x, 2160 × 1026, sitting at y -500 on a cover, y 816 on a content
slide, y -642 on a closer.

**The wash is smooth.** Nothing is laid over the colour. A hero that carries a
second layer is wrong, and the fix is to delete that layer rather than to tune
it.

One deliberate departure from Figma, for a reason worth knowing:

- **The progressive blur becomes a flat blur.** CSS has no progressive blur.
  Use `filter: blur(34px)` at native size on the wash layer, which is the whole
  of the hero, at roughly the mid-band radius.

In CSS the whole thing is one pseudo-element, which means the markup stays
`<div class="hero"></div>` and no template needs editing:

```css
.hero {
  position:absolute; left:-64px; top:-210.7px; width:922px; height:438px;
  overflow:hidden; background:var(--white);
}
.page--cont .hero { top: 964.3px; }

.hero::before {
  content:""; position:absolute; top:0; left:0; height:684px;
  transform:scale(0.6403); transform-origin:top left;
  left:-64.03px; width:1751px; filter:blur(34px);
  background:
    linear-gradient(180deg, #fff 0%, #fff 19%, rgba(255,255,255,.78) 28%,
      rgba(255,255,255,.38) 40%, rgba(255,255,255,0) 48%,
      rgba(255,255,255,.18) 70%, rgba(255,255,255,.86) 84%, #fff 90%),
    linear-gradient(92.24deg, #FF5331 0.07%, #FCE1DA 38.25%,
                              #9CDFF3 75.92%, #D8F6FF 89.42%);
  opacity:.8;
}
```

The vertical white profile in `::before` is not decoration either. It encodes
where the wash is legible: hero local 0 to 130 is above the gradient rectangle
and reads white; the wash ramps in from 130 to 330; it holds to about 510 and
is gone by 600. Page 1 shows local 329 upward, which is why its head is at full
strength. A continuation page shows local 0 to 248, which is why its foot is
pale. Both come from the same profile. If you flatten it, page 1 stays right
and every later page grows a hard saturated band across its bottom.

### 4e. Bar comparison

Rounded track in `--wash`, teal gradient fill, label left, value right. Widths
are set inline as percentages so the ratio is the claim: if Keeyu does 5 to 10
days of work and the customer does 2 to 3 hours, the customer bar is 4 percent,
not 20. The graphic is the argument.

---

## 5. Placeholder contract

Every template is consumed by a Python renderer that does a literal string
replace of `{{TOKEN}}`. Two rules follow:

1. **Never change a template's placeholder set** without changing the renderer.
   Before shipping any rebuilt template, diff its tokens against the old one.
   Same set, same spelling, or the renderer breaks for every customer.
2. **Never let `{{ }}` appear in a comment.** A strict unfilled-placeholder
   audit is a plain regex over the file and it cannot tell a comment from
   markup. Writing `rather than taking BASE_CSS` in braces in an explanatory note
   makes the audit report a missing variable forever. Strip the braces in prose:
   write `BASE_CSS`. This has regressed twice.

Audit before delivering:

```python
import re
left = sorted(set(re.findall(r'\{\{([A-Z0-9_]+)\}\}', open(f).read())))
```

The only names that should come back are ones the renderer supplies.

---

## 6. Rendering to PDF

**Do not use Chromium's print path.** `page.pdf()`, "Save as PDF" and every
headless print route re-rasterise through a pipeline that does not honour
`filter`, `mask-image` or `clip-path`. Those three are what the hero wash, the
gradient-edged cards and the page dot grid are built from, so a printed PDF
quietly loses all of them. This was diagnosed by rendering both ways and
comparing, not guessed.

Render by photographing the page in a real browser and placing the images on
correctly sized pages:

```js
const ctx = await b.newContext({ viewport: { width: 2000, height: 1400 },
                                 deviceScaleFactor: 3 });   // 3x = 288 dpi on A4
const p = await ctx.newPage();
await p.goto('file://' + input, { waitUntil: 'domcontentloaded' });
await p.evaluate(() => document.fonts.ready);               // load bearing, see below
for (const sheet of await p.$$('.sheet'))
  await sheet.screenshot({ path: out, scale: 'device' });
```

Then assemble with `img2pdf`, deriving each PDF page size from the sheet's own
CSS size (CSS px are 1/96 in, PDF points 1/72, so multiply by 0.75) and snapping
to exact A4 when it lands within a point.

The trade is that type is raster rather than selectable and the files are
larger. For a design reference that is the right trade, and it is the only way
these pages come out of a PDF looking like they do in a browser. If a
searchable-text PDF is genuinely needed, print from a browser by hand.

A working implementation ships with the `keeyu-pdf-conversion` skill:
`shoot.js`, `shots2pdf.py` and `build_pdfs.sh`.

### Fonts at render time

Wait for `document.fonts.ready` before shooting, and use the **variable**
families. Optical sizing is load bearing: a static Roboto Serif sets display
type about 8 percent wide, which pushes headings onto extra lines and drops
them onto the content below. Text collisions that do not exist in the Figma
source are a font problem before they are anything else.

### Verify, always

Never deliver a PDF you have not looked at. Rasterise it and read the pages:

```python
import pypdfium2
d = pypdfium2.PdfDocument(path)
print(len(d), [pg.get_size() for pg in d])
for i, pg in enumerate(d):
    pg.render(scale=2).to_pil().save(f'_p{i}.png')
```

Page count and page size catch the two failures that matter: content overflowing
into a phantom third page, and landscape silently rendering portrait.

---

## 7. Density on the page

The standing instruction from the client is absolute: **always index on more
information density, less white space.** It applies to HTML exactly as it
applies to Figma.

In practice this means: after rendering, look at the bottom of every page. If
there is more than roughly a quarter page of dead space, the page break is in
the wrong place. Pull the next heading and its first block up onto the page.
A section heading with its lead-in row at the foot of one page and its captioned
graphic opening the next is correct and normal. A page that stops two thirds of
the way down is not.

Do not solve dead space by growing the type or adding leading. Move content.

---

## 8. Building a template from scratch

The order below is not negotiable, because the failure that got a whole set of
eleven templates rejected was doing step 3 before step 1.

1. **Open the Figma document the template renders.** Screenshot every page.
   The template mirrors that document block for block, in that order, with that
   copy. It is not a fresh design that happens to use Keeyu colours.
2. **Extract every graphic** on those pages via `get_design_context` (section 1).
3. **Write the file in one pass.** Assemble the whole document and write it
   whole. Do not build a template by successive regex surgery on an existing
   one: that is how a two-page brief silently became three pages with a
   duplicated section. If a template needs structural change, rewrite it.
4. **Inline the stylesheet.** The renderer substitutes the base CSS into a
   `<style>` block; the delivered HTML is self-contained with no external
   stylesheet.
5. **Audit placeholders** (section 5).
6. **Render and read the pages** (section 6).
7. **Check density** (section 7).

### File anatomy

```
<!DOCTYPE html>
<html><head><meta charset="utf-8">
<style>  ← full keeyu_base.css, then a short note comment, no {{ }} in it
</style></head>
<body>
  <div class="page">            ← page 1, carries the hero wash
    <div class="hero"></div>
    <img class="logo" src="LOGO_BLACK_PATH">
    <div class="content"> ... </div>
    <div class="doc-footer"><span>Doc name</span><span>1 / n</span></div>
  </div>
  <div class="page page--cont"> ← every later page
    ...
  </div>
</body></html>
```

`assets/example_tech_integration_brief.html` is a complete worked example of
this anatomy, with the systems graphic in place. Read it before writing a new
one.

---

## 9. Environment limits, known and permanent

- **The proxy blocks figma.com asset traffic** (403 on CONNECT). Exported SVGs
  cannot be downloaded and images cannot be uploaded. Every vector must be
  reauthored from the geometry `get_design_context` returns. Photographs and
  logo grids are dropped in by hand by the designer; leave a captioned gap and
  say so, do not fake them.
- **`use_figma` returns no values in some sessions.** When it does, read state
  back by writing the data into a known node's `name` and reading it with
  `get_metadata`.
- **`use_figma` scripts cap at 50,000 characters** and the MCP call times out at
  60 seconds. One page per call.
- **Geist is not yet licensed for PDF embedding.** Until the licence is cleared
  and the font is in `10_Brand_Assets/fonts/`, templates load it from Google
  Fonts at render time. Flag this on any document going to print.

---

## 10. The stylesheet

`assets/keeyu_base.css` is the whole system and ships with this skill. Inject it
verbatim; do not fork it per template. Its sections:

    1  Fonts                     11  Graphic well
    2  Design tokens             12  Closing blocks
    3  Page setup                13  Landscape pages
    3b Flowing document          14  Deck slides
    4  Hero wash                 15  Shared A4 components + renderer aliases
    5  Furniture                 16  Prose section block
    6  Content column            17  Bar comparison
    7  Type ramp                 18  Graphic modules (.fig-scale + systems)
    8  Rules                     19  Next-step card
    9  Stat row
    10 Comparison rows

Section 15 matters: it aliases the legacy renderer class names (`.cs-*`,
`.ar-*`, `.csa-*`, `.map-*`) onto the shared components, which is why the v4
rebuild required no Python changes. Keep those aliases when editing.

---

## 11. Reproducing a Figma page in HTML: what actually bites

Learned by cloning the ten Figma documents into HTML and rendering all 44 pages,
2026-08-07. Each of these produced a visible defect that survived a first review.

**Auto-width text must not wrap.** A Figma TEXT node with
`textAutoResize = 'WIDTH_AND_HEIGHT'` grows with its string and cannot wrap. Give
it `white-space: pre`. With `pre-wrap` it wraps the moment metrics differ by a
hair, and the second line lands on whatever sits below: this put "mo" through
"Payback period" and "weeks" through "Payback period" on four documents.

**A clipping frame must stay a container.** Flattening the tree to absolutely
positioned siblings drops `clipsContent`. The hero is a 1751px wash cropped to
a 684px window; unclipped it runs a third of the way up the page as a band of
colour across the content. Keep an explicit clip.

**The hero's vertical white profile is not optional.** The wash is not a plain
gradient rectangle: the base stylesheet layers a white fall-off over it,
alpha 1 at the head of the hero, clear across the middle where the wash is
meant to read, and back to 1 before the foot. That profile is what confines the
wash to a band. Serialised flat it disappears, and the wash then sits at full
strength across the entire 684px hero. On a page-1 hero, where only the lower
part shows, that looks almost right. On a continuation-page hero, where only
the top 248px shows, it is completely wrong: the foot of every page prints as a
hard, saturated cyan band instead of the pale whisper the design has. Rebuild
the profile as a mask in the wash's own coordinate space.

**The hero's white fade is a real node, and it is the paper.** Every hero
carries a white-to-transparent rectangle over the bottom 379px of its 684px
height, opaque at the hero's foot. That is the trailing half of the vertical
profile, and it is the reason the wash does not cut hard at the crop on a
page-1 hero. Two consequences. It is pure white, so the moment the page ground
stopped being white it printed as a lighter panel with a visible edge where the
hero crop ends: it must carry the paper colour, not #FFFFFF. And because it
sits at the hero's foot it is entirely off-page on a continuation hero, which
is why only the leading half of the profile needs rebuilding as a mask.
Rebuilding the whole profile doubles up with this node.

**Layer blur has no CSS equivalent.** Figma's PROGRESSIVE blur on the hero wash
must be substituted with a flat `filter: blur()`, at 34px for the A4 hero's
native 1751 width.

**A gradient stroke is a border, not a fill.** A transparent border plus
`background-image` paints the gradient across the whole box and turns a white
card with a hairline edge into a solid slab. Use the two-layer form: the node's
own fill clipped to `padding-box`, the gradient clipped to `border-box`. And
check for a second stroke: a node can carry a flat grey plus a gradient, and
reading only the first loses the treatment entirely.

**Vectors are not boxes.** A dashed elbow connector drawn as its bounding box
becomes a solid rounded rectangle, and a vector rotated -90 drawn at its
unrotated dimensions lands horizontally across the wrong column. Export the node
from Figma with `exportAsync({format:'SVG'})` and place the real geometry.

**The wordmark is nine vector nodes.** Reproduced as boxes it renders as nine
black blocks. Place `keeyu-logo-black.svg` at the cluster's measured bounds; use
the white variant on dark grounds.

**A hairline artefact at the hero crop, fixed 2026-08-07.** Worth knowing
because it is invisible at thumbnail size and obvious on paper.

It is a coloured hairline at the bottom edge of the page-1 hero. The
wash rectangle's bottom edge lands exactly on the crop, at full strength, so it
cuts hard. In Figma the PROGRESSIVE blur has dissolved it before it reaches the
edge; a flat blur cannot. Carry the dissolve as a mask on the wash instead:
solid through the top half, gone by the bottom edge. Same intent as the
vertical white profile in the base stylesheet.

It is found by scanning a render for a row far darker than its neighbours, in
the page margin where only background appears. Do that before shipping a
rebuild.

**Figma soft breaks are U+2028.** Chromium does not break on U+2028 in
`white-space: pre-wrap`, so the break silently becomes a space and the line
rewraps somewhere else, leaving a visible double space. Convert them to
newlines. They also arrive through tooling rendered as a plain space, so they
are easy to lose in transit.
