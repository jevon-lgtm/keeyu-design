# Keeyu Components

> Build recipes with exact geometry. Values come from `design-tokens.md`; this
> file says how they assemble.

## Page shell

Every page:

1. Frame 1240 × 1754, fill `#FFFFFF`, `clipsContent = true`.
2. Page 1 only: the hero glow group (see design-tokens).
3. Logo instance at (89, 70), 130 × 30. If the Keeyu logo component is not
   available in the file, place the wordmark and symbol from
   `10_Brand_Assets/brand/wordmark-symbol/`. Never redraw the mark from
   primitives in a final document.
4. Footer at y 1696: artefact name left at x 84, `n / total` right-aligned at
   x 1036. Both Geist Regular 13 `muted`.
5. Content column: vertical auto-layout, width 1072, at (84, 146), itemSpacing 0.
   All vertical rhythm comes from per-block top padding, never from itemSpacing
   on the column.

## Header block

Vertical auto-layout, gap 20.

- Document title, Roboto Serif Light 72
- Meta line, Geist Regular 19 `body`, format: `Customer   ·   Artefact: Month Year`
  with three spaces either side of the middle dot

Followed by the divider block: a padding-only wrapper (top padding 40, no fill,
no stroke) containing a real 1 px `rule` **`LINE` node** at full content width:
`figma.createLine()`, `resize(1072, 0)`, stroke `rule` `#E0E0E0`,
`strokeWeight = 1`. Never a rectangle, and never a frame with a bottom border.
See non-negotiable 9 and technique 6 in SKILL.md.

## Intro paragraph

Wrapper with top padding 30, **fixed width 780** (not full content width).
Geist Regular 17, `body`, line height 140%.

## Stat row

Wrapper top padding 48. Horizontal auto-layout, **width 695**, `SPACE_BETWEEN`.
Each column hugs, vertical, gap 4, and is **centre aligned**: set
`counterAxisAlignItems = "CENTER"` on the column and
`textAlignHorizontal = "CENTER"` on both texts. The label is usually wider than
the numeral, so left alignment leaves the numerals visibly adrift.

- numeral: Roboto Serif Light 54, `ink`, centred
- label: Geist Regular 14, `muted`, centred

Four stats maximum. Labels are two or three words. No containers, no dividers
between them.

**The 695 width assumes short numerals.** Measure first: if the four numerals
together exceed about 600 px, as they do when two of them are six-figure dollar
amounts, widen the wrapper to the full content width instead. Numerals colliding
with their neighbours is the failure this prevents. Never shrink the numeral to
make 695 work.

## Section heading

Wrapper top padding 50 to 62. Roboto Serif Light 40, `ink`, tracking -0.2%.
Use 62 when the heading follows a stat row, as in What We Heard. Use 50 when it
opens a prose document, as in the Tech Integration Brief.

## The two block families

Every Keeyu body block is one of two shapes. Do not mix them inside one section.

**Comparison row** — the What We Heard block. Two 514 columns, a situation on
the left and the mechanism on the right. Use only when the document genuinely
argues problem against fix.

**Prose section block** — the Tech Integration Brief block. One headline over
one 880 px paragraph. Use for everything explanatory: how something works, what
is included, what is not, what happens next. This is the more common of the two.

Both are separated by standalone rules, never by frame borders.

## Prose section block

The default block for non-comparison documents. Blocks live in a vertical
auto-layout column with **itemSpacing 30**, each pair separated by a standalone
1 px `hair` rule.

1. **Headline** — Roboto Serif Light 32, `ink`, tracking 0, full content width.
2. **Body wrapper** — vertical, gap 12 from the headline, **fixed width 880**.
   Geist Regular 15, `body`, line height 140%, tracking -0.2%.
3. **Graphic block** (optional) — vertical, top padding 46, gap 20.
   Serif caption 19.4 `ink`, then the graphic well.

Note the body colour: prose section blocks use `body` `#4D5454`, not the
`soft` / `strong` pair that the two-column comparison row uses.

## Label and value row

Used where the document lists confirmed inputs, as in the ROI Breakdown's first
column. Horizontal auto-layout, `SPACE_BETWEEN`, full column width, vertical
padding 14, with a standalone 1 px `hair` rule between each pair.

- label left, Geist Regular 15, `soft`
- value right, Roboto Serif Light 19.4, `ink`, right-aligned

Never a table, never zebra striping, never cell borders.

## Vertical stat stack

The portrait stat row turned on its side, for a narrow column. Each entry is a
vertical auto-layout, gap 4, with a standalone rule between entries and 26 px
padding above and below:

- numeral Roboto Serif Light 54, `ink`, tracking -1%
- label Geist Regular 14, `muted`, line height 150%

## Comparison row

The core repeating block, measured from the approved Business Case page 3. The
headline sits **beside** the content, not above it, and the two halves of the
comparison stack **vertically** in the right-hand column.

Separator between rows: a padding-only wrapper with **30 top and 30 bottom**
padding containing a full-content-width `rule` line. Not top-padding-only, and
not a border on the row.

The row itself is a **horizontal** auto-layout at the content width,
`SPACE_BETWEEN`, counter axis `MIN`, carrying no strokes and no padding. Measured
gap between the two columns is 107.

1. **Headline column** — fixed 444 wide. Roboto Serif Light 34, `ink`,
   line height 124%, tracking -0.2%. It wraps to two lines often; that is
   correct and is why it gets its own column.
2. **Response column** — fixed 514 wide, vertical, itemSpacing 15, holding
   three children:

   a. **Situation block** — label then prose, gap 0.
      Label, for example "Pain point": Geist Medium **18**, `coral`,
      line height 150%.
      Prose: Geist Regular 15, `soft`, line height **130%**, tracking -0.2%.

   b. **A `rule` line**, 514 wide, 1 px `hair`. This is the only rule inside a
      row.

   c. **Response block** — same shape.
      Label, for example "How Keeyu solves this": Geist Medium 18, `teal`,
      line height 150%.
      Prose: Geist Regular 15, `strong`, line height 130%, tracking -0.2%.

Both labels appear on **every** row, not once at the top.

**Graphic block** (optional) — a sibling below the row: vertical, top padding
20, gap 15, serif caption 19.4 `ink`, then the graphic well.

Note the deltas from the older stacked form: the headline moved beside the
content rather than above it, column labels went from 17 to **18**, the
situation label went from `muted` to **`coral`**, and comparison prose runs at
**130%**, not the 140% used everywhere else in the system. The tighter leading
is what lets two stacked blocks sit in a 514 column without the row growing past
its headline.

The coral and teal labels are the brand rule doing real work: `coral` names the
problem, `teal` names the resolution, on every row. That pairing is why the
labels repeat rather than sitting once at the top of the section.

## Graphic modules

Pick the module whose shape matches the claim. All five sit in the standard
graphic well: 1072 wide, `#F9F9F9`, 1 px `#ECECEC`, radius 22.

### 1. Progress timeline
**Use for:** several parallel things running to different completion states.

Well height 218. Rows at y 34, 92, 150 (58 px pitch).

Per row:
- label at x 44, Geist Regular 15 `strong`, vertically centred on the bar
- track: x 250, width 682, height 34, radius 10, fill `track`
- fill bar: same x/y/height/radius, width = 682 × percentage, coral or teal
  gradient with the horizontal bar effects
- status at x 954, Geist Regular 14, `coral` when at risk, `muted` otherwise

Use coral for the one that is failing and teal for the rest. Never more than
four rows.

### 2. Systems we connect to
**Use for:** Keeyu sitting above the customer's existing stack. This is the
single most reused graphic in the library and it appears in nearly every
artefact, so it is **standardised**: clone the approved instance and retype the
five card labels and the caption. Do not rebuild it from primitives, and do not
redesign it per document.

Well height 268, full content width.

- **Keeyu pill**: x 432, y 42, width 208, height 58, radius 12. Fill is the
  **brand 4-stop gradient**, not flat teal. Effects: `INNER_SHADOW` `#FFFFFF`
  y1 r0, plus `DROP_SHADOW` `#3FA7B7` @0.55 y10 r20 spread -8.
- **Label** "Keeyu": Geist Medium 19, `body` `#4D5454`, centred across the full
  well width so it lands centred on the pill. Not white, not on a teal fill.
- **Connectors**: dashed vector elbows, 2 px `connector` `#CBCBCB`, dash
  pattern `[4, 4]`, corner radius 12 to 20. They branch from under the pill out
  to each card, they are not straight vertical drops.
- **Cards**: five, y 152, height 66, width 184, at x 44, 244, 444, 644, 844.
  White card recipe, radius 10. Label centred, Geist Medium 14, `strong`.
- **Caption** inside the well at x 44, y 232, Geist Regular 14, `muted`.

Five cards is the shape. If the customer has fewer named systems, group the
tail into one card such as "Carriers". If they have more, group as well: this
graphic says "one layer over your stack", not "an exhaustive inventory".

### 3. Quantity comparison
**Use for:** a before/after count. Two bars, nothing else.

Well height 286. Bars are vertical, bottom-aligned, centred as a group.

- Larger bar: width 84, height proportional (152 for a 4), radius 12, coral
  gradient, vertical coral effects. Numeral centred inside, Roboto Serif Light 34,
  `white`, sitting in the upper third of the bar.
- Smaller bar: width 84, height proportional (46 for a 1), radius 12, teal
  gradient, vertical teal effects. Numeral Roboto Serif Light 26, `white`.
- Labels below both bars, Geist Regular 14, `muted`, centred on the bar.

No arrow, no big numerals repeated beside the bars, no axis. The two bars
carry it.

The 84 px bar width assumes a one or two character numeral. A bar carrying
`$662,000` needs about 168. **Widen the bar to fit the numeral; never shrink the
numeral to fit the bar.** If the numeral still wraps, the claim wants the
horizontal bar treatment of the progress timeline instead.

### 4. Metric cards
**Use for:** a small set of things now being measured or delivered.

Well height 172. Three cards, y 28, height 84, radius 12, white card recipe,
evenly distributed across the well with 44 px outer padding.

Inside each card, x offset 22 from the card edge:
- title at y 50, Geist Medium 16, `strong`
- status at y 74, Geist Regular 13.5, teal gradient fill on the text

Caption inside the well at x 44 near the bottom, Geist Regular 14, `muted`.

### 5. Attribute cards
**Use for:** parallel entities each with two or three attributes.

Well height 227. Four cards, y 39, height 114, radius 12, white fill, **gradient
border** using the brand 4-stop with the card border transform, plus the white
card shadows.

Inside each card, x offset 23:
- name at y 62, Geist Medium 18, `strong`
- primary attribute at y 87, Geist Regular 15, `soft`
- secondary attribute at y 108, Geist Regular 13.5, `muted`

Caption inside the well at x 44 near the bottom, Geist Regular 14, `muted`.

## Closing blocks

"In short" and "Next step: …" are pain-row siblings without the two-column
structure:

- a standalone 1 px `hair` rectangle above the block, never a border on it
- wrapper top padding 54, no strokes
- heading Roboto Serif Light 34, `ink`
- body Geist Regular 16, `body`, line height 140%, constrained to 880 px

Never put the closing blocks in a well or a tinted panel.

## Deck graphic modules

Two modules exist only at deck scale. Both are wells, so both follow the well
recipe: fill `wellBg`, 1 px `hair` stroke, radius 22, `clipsContent` true, with
a Geist Regular 19 `muted` caption at the bottom left inside.

### Order-journey card row

For a claim shaped as a sequence of stages across systems. The well runs the
full 1680 content width. Inside, a dashed `connector` line runs behind the cards
at their vertical centre, and the cards sit on it.

```
well      1680 × 400 to 440, inner padding 40
cards     n across, white, 1 px cardBorder, radius 10 to 12,
          one DROP_SHADOW #000000 @0.05 y3 r6
          five stages  -> 290 wide, 250 tall, pitch 326
          nine stages  -> 160 wide, 180 tall, pitch 180
card text title Geist Medium 17 to 20 `strong`
          body  Geist Regular 15 to 16 `soft`, 150%
connector dashPattern [6,6], stroke `connector`, spanning the card row
```

When the row carries a direction, label the two ends: `coral` at the start
(customer promise, the thing at risk) and `teal` at the end (promise kept).

### Positioning matrix

For a claim shaped as two axes. The well is 1680 × 600. Two dashed `connector`
lines cross at the centre; four white cards, 560 × 200, sit in the quadrants at
x 220 and 900, y 80 and 360. Axis labels are Geist Regular 17 `muted`, placed
just inside the well edge, never on it: keep 40 px of clearance or the text
renders on top of the border.

Each card carries a Geist Medium 22 `strong` title, a Geist Regular 17 `body`
description, and a Geist Regular 17 list of the players in that quadrant. Colour
that last line only where the quadrant is a judgement: `teal` where Keeyu sits,
`coral` for the reactive quadrant, `soft` everywhere else.

---

## Page dot grid

On every A4 page, sitting directly above the hero and below all content. In
Figma it is a frame named `dot grid` at page size, clipping its contents, with
three children in this order:

1. `fade`, a rectangle set as an alpha mask (`isMask = true`), linear gradient
   running top to bottom, stops at `design-tokens.md`.
2. An instance of `Texture / Dot Grid Page 1240x1754`.
3. `scrim`, a rectangle 1239 x 1736 at (1, 9), **paper coloured** (#FAFAFA),
   opaque at the top of the page fading to clear at the foot, painted **over**
   the dots and inside the same mask.

Z-order follows the hero: **under** a hero at the head of the page so the wash
stays clean, **over** a hero at the foot so the texture carries across it. Page
1 of every document is the first case, every continuation page the second.

It goes on **every document frame in the Figma file**, portrait and landscape,
not just the documents that have HTML templates. 55 A4 frames across 13 document
pages as of 2026-08-07, then extended on 2026-08-16 to every landscape page:
the 15 frames on Doc 3 ROI Breakdown, Doc 5 The Offer, Doc 10 Demo Deck and
Doc 12 Assumptions Register, and the 27 slides of Attachments 1, 3 and 4.

Landscape uses `Texture / Dot Grid Page 1920x1080`, which tiles 20 instances of
the same canonical `Texture / Dot Grid Tile 400x300` at its **native geometry**.
The dot pitch stays 20 units on either orientation. Do not rescale the tile for
landscape: it would force a per-orientation `background-size` in the HTML and
let Figma and the templates drift apart. The consequence, worth knowing, is that
a 20-unit pitch is 12.8 CSS px on A4 at the 0.6403 constant and 20 CSS px on a
landscape page at scale 1, so the texture is physically coarser on the decks.

The scrim inset is the same 1 px left and 9 px top and bottom on both, giving
1239 x 1736 on A4 and 1919 x 1062 on landscape. Derive it from the frame rather
than hardcoding the A4 figures.

Deliberately excluded: the `Texture / Dot Grid Page` components on the Reference
page, since applying a dot grid to the dot grid would be circular; the `spare`
deck; loose graphics and logo rectangles sitting on a page canvas rather than
inside a document frame.

**Judge z-order by clipped coverage, not by the hero's midpoint.** Clip the
hero to the page and measure what fraction of the page height it covers. Over
about **80 per cent** is a full-page hero and takes the dots **above** it, or
the hero's opaque ground hides them completely. Under that, the midpoint rule
applies: hero at the head of the page takes the dots below, hero at the foot
takes them above.

The midpoint test alone is wrong and has been caught in the file. `Slide 17` on
Attachment 1 and `Slide 10` on Attachment 4 both carry a hero from y -4 to 1022
on a 1080 page. Their midpoint sits above centre so a midpoint test calls them
head heroes and buries the grid, when in fact the hero covers 94.6 per cent of
the page. Every Doc page passes either test, the deepest being 48.7 per cent on
Demo Deck slide 1, which is why the fault only appeared on the attachments.

**There are two stacked falloffs, not one.** This is the part that gets missed.
The alpha mask on its own is far too gentle to read at these dot values, and
the obvious compensation, darkening the dots, produces a texture that is too
heavy at the foot and still does not read as a gradient. The scrim is what
makes the falloff legible while the dots stay light. If someone reports that
there is no gradient, do not reach for the opacity: check the scrim is present,
then measure the render in the page margin where only dots appear.

In HTML the whole thing composes into one rule, two background layers under a
mask:

```css
.dot-grid { position: absolute; left: 0; top: 0; width: 1240px; height: 1754px;
  background-image:
    linear-gradient(to bottom, rgba(250,250,250,1) 0%, rgba(250,250,250,0) 100%),
    radial-gradient(circle, rgba(0,0,0,.08) 1.5px, rgba(0,0,0,0) 1.75px);
  background-size: 1239px 1736px, 20px 20px;
  background-position: 1px 9px, 0 0;
  background-repeat: no-repeat, repeat;
  mask-image: linear-gradient(to bottom, rgba(0,0,0,0) 0%, rgba(0,0,0,.06) 35%,
                              rgba(0,0,0,.225) 70%, rgba(0,0,0,.5) 100%); }
```

`background-size: 20px` with the dot centred puts a 1.5px dot at 10,10 in every
cell, which is exactly where the Figma tile places it.

Do not hand-place dots, and do not serialise the tile out of Figma: each tile is
one vector carrying 300 bezier circles, which exports as a grey box and explodes
to thousands of nodes if flattened. Author it as the CSS rule above.


---

# Chips, boxes and grids

Four components added 2026-08-17. They are the difference between a document
that is merely correct and one that reads as finished. Reach for them in the
situations named below rather than inventing a new treatment.

## Chip

A status, a track name, a milestone label or a list numeral. Geometry and
colourways are in `design-tokens.md`. Use it for:

- **A status column.** `Answered` / `Open` / `Confirmed` on a log, a checklist
  or a register. Right-align it by setting the cell's
  `counterAxisAlignItems = "MAX"`.
- **Table column headers** where the header names a parallel option, such as the
  three subscription tracks.
- **A term label** in a schedule row, where the left column names a milestone.
- **A list numeral**, at 1.3x. See the two-column numbered list below.

Coral means open or a problem, teal means confirmed or resolved. A checklist
therefore ships with every row coral, and a confirmation document with every row
teal. Never mix the two meanings on one page.

Prose still never sits in a chip. A chip carries a token: one to three words, or
a numeral. If it would wrap, it is not a chip.

## Gradient border box

Wrap a **table** in it. Geometry is in `design-tokens.md`. Use it for the
subscription fees table, a guarantees comparison, a checklist, a contacts table,
a cadence confirmation. Do not wrap prose, schedule rows or a graphic well in
it: schedule rows stay open on the page and a well already has its own
container.

One box per page reads as emphasis. Three boxes stacked read as a form.

## Tile grid

Use it wherever the source gives a **list of categories each with a value**:
systems by type, integrations by layer, tools by lifecycle stage. It replaces a
run-on list, which is the weakest thing in the system.

    well     VERTICAL, itemSpacing 24, padding 28 / 44, wellBg fill,
             1 px hair stroke, radius 22, FILL width, HUG height
    row      HORIZONTAL, itemSpacing 24, FILL width, HUG height, counter MIN
    tile     VERTICAL, itemSpacing 6, padding 22 all round, #FFFFFF fill,
             brand gradient stroke 1 px, radius 12, card shadows, FILL horizontal
    label    Geist Medium 16, `strong`
    detail   Geist Regular 14, `soft`, 140%

Three tiles to a row divide the 984 inner width into 312 each. **Set every tile
to `layoutSizingVertical = "FILL"`** against a hugging row: the row takes the
height of its tallest tile and the others stretch to match, so the row is flush
without measuring anything. Build it entirely in auto-layout, never by absolute
x and y, so adding a seventh category reflows the grid on its own.

The tile grid answers a different question from the systems graphic and the two
can sit on one page: the grid is the inventory, the graphic is the claim that
Keeyu is one layer over it. If the page is heavy, the graphic is the one to cut.

## Two-column numbered list

The form for **any numbered list of five or more items**. A single full-width
column at 880 sets lines too long to scan and wastes the right half of the page.

    wrap     HORIZONTAL, itemSpacing 45, paddingTop 25, HUG width, counter MIN
    column   VERTICAL, 450 FIXED, itemSpacing 22, paddingTop 12, counter MIN
    item     HORIZONTAL, itemSpacing 19, FILL width, counter MIN
    numeral  a 1.3x chip inside a hugging holder frame
    body     Geist Regular 15, `body`, 150%, -0.2%, FILL

The two columns hug to 945 inside the 1072 content width. Split the items
`ceil(n / 2)` left and the remainder right. **The columns do not have to end
level**, and padding the shorter one to match is wrong.

Numerals follow the brand rule: **coral where the list names problems**, teal
where it names objectives, fixes, priorities or resolutions.

Keep the numeral in a holder frame rather than putting the chip straight in the
row. The holder is what lets you change the gutter without touching 24 items,
and hugging it is what pulls the chip tight to its text.
