# Keeyu Design Tokens

> Every value here is measured from the approved reference document. These are
> exact values, not guidance. Do not scale, round or substitute.

## Canvas

| Property | Value |
|---|---|
| Page size | 1240 × 1754 px (A4 portrait at 150 DPI) |
| Page fill | `#FFFFFF` |
| Margin | 84 px left and right |
| Content width | 1072 px |
| Content column origin | x 84, y 154 |
| Prose column width | 514 px each, gap 44 px |
| Logo position | x 89, y 70, size 130 × 30 |
| Footer baseline | y 1696 |
| Footer left text | x 84 |
| Footer right text | x 1036, right-aligned, width 120 |

Content must clear y 1696. If it does not, break to a new page. Never shrink
type or tighten leading to force a fit.

### Landscape variant

Only the ROI Breakdown uses this. Everything else is A4 portrait.

| Property | Value |
|---|---|
| Page size | 1920 × 1080 px |
| Margin | 120 px left and right |
| Content width | 1680 px |
| Content origin | x 120, y 146 |
| Columns | 3 × 520 px, gap 60 |
| Logo position | x 125, y 70, size 130 × 30 |
| Footer baseline | y 1022 |
| Footer right text | x 1680, right-aligned, width 120 |

**Landscape documents keep the A4 type ramp.** The ROI Breakdown and The Offer
are read on a laptop at arm's length, so the canvas gets wider and the type does
not.

### Deck scale

The Demo Deck is the one exception, because it is projected and read across a
room. It uses a **1.35× ramp**, applied to every text token except the footer:

| A4 | Deck |
|---|---|
| 72 (title) | 96 |
| 40 (section) | 54 |
| 34 | 46 |
| 32 (headline) | 44 |
| 19.4 (caption, quote) | 26 |
| 54 (stat numeral) | 72 |
| 18 | 24 |
| 17 (intro) | 22 |
| 15 (body) | 20, at 152% line height |
| 14 (label) | 19 |
| 13 (footer) | 15 |

Text columns narrow to match so paragraphs still run several lines deep: the
three-up goes 520 → 468 with a 138 gutter, the four-up 800 → 740 with a 200
gutter. A graphic cloned from an A4 document keeps its native 1072 width and is
**centred** in the 1680 column. Stretching it to full width leaves its contents
stranded on the left, because the children do not reflow.

This scale applies to the Demo Deck **and every other 1920 × 1080 deck**,
including the Sales Deck Outline and the email-attachment decks. They are one
family and must be interchangeable at a glance.

### Deck slide grid

Measured off the approved Demo Deck. Every content slide is laid out on this
grid. There is no second deck layout.

| Element | Value |
|---|---|
| Margin | 120 left and right, content 1680 |
| Logo | x 125, y 70 |
| Slide title | Roboto Serif Light **54**, x 120, y **140** |
| Divider under the title block | full-width 1680 line, `rule` colour |
| First content row | y 390 |
| Content bottom | ends by y **960**. The footer sits at y 1022 |
| Two-up | 740 wide, 200 gutter: x 120 and x 1060 |
| Three-up | 468 wide, 138 gutter: x 120, 726, 1332 |
| Four-up | 360 wide, 80 gutter: x 120, 560, 1000, 1440 |
| Statement / pull quote | Roboto Serif Light 44 |
| Section head inside a slide | Roboto Serif Light 44 |
| Column label | Geist Medium 24, `coral` or `teal` for a paired column, `strong` otherwise |
| List item | Geist Regular 24, `strong`, with a `hair` line above each item |
| Body paragraph | Geist Regular 20 at 152%, `body` |
| Stat numeral | Roboto Serif Light 72 over a Geist Regular 19 `muted` label |
| Label / value row | Geist 20 `muted` label left, Roboto Serif Light 32 value right, line under |

**The title is 54, not 96.** 96 is the cover only. A content slide that opens
with a 72 or 96 display line does not belong to this deck. Where a merge puts a
second head on a slide, demote it: 54 title, 44 section.

A slide that stops at y 700 is unfinished. The last element lands between
y 900 and y 966; do not leave the bottom third bare and do not push past the
footer.

**Index on density, always.** When a slide has room left, the answer is never a
bigger gap. In order of preference: run the columns wider, set the type a step
larger, or go back to the source and find the content that belongs there. A
placeholder box, a two-line slide, or a column that stops halfway is a slide
that has not been finished. Where an asset cannot be reproduced, transcribe what
it says and build the content in type rather than leaving an empty frame.

### Paired-column form

The Keeyu deck's signature slide, measured from Demo Deck slide 4. Use it
whenever two lists answer each other item for item.

```
left column   x 120, width 790
right column  x 1010, width 790
divider       a vertical LINE at x 950, hair, spanning the item stacks
              (createLine, resize(len,0), rotation = -90)
item numeral  Geist Regular 17, coral on the left, teal on the right
item text     Roboto Serif Light 27 to 32, soft on the left, strong on the right
              numeral to text 26, item to item 16 to 22
column label  Geist Medium 24, coral or teal, above the stack
tail line     Geist Regular 19, muted, under the stack
```

The two columns do not have to end level. The left list being longer than the
right **is the argument**. Do not pad the shorter one to match.

Where the source title splits naturally across the pair, split it: the left
column takes the first half in `ink`, the right takes the second in `muted`.

When an item carries a headline and a body rather than a single phrase, the item
becomes numeral, then Roboto Serif Light 44 headline, then Geist Regular 19 body
at 150%, on a pitch of about 157.

## Colour

| Token | Hex | Use |
|---|---|---|
| `ink` | `#000000` | Display type: doc title, section heading, pain headline, stat numerals, graphic captions |
| `strong` | `#1A1A1A` | The Keeyu-response prose column; titles inside graphic cards; bar row labels |
| `body` | `#4D5454` | Intro paragraph, meta line, closing prose |
| `soft` | `#797E82` | The "what we heard" prose column; secondary line in market cards |
| `muted` | `#9AA0A6` | Stat labels, column label (left), captions inside wells, footer, neutral status |
| `rule` | `#E0E0E0` | The main divider under the header |
| `hair` | `#ECECEC` | Every rule and row separator (always a `LINE` node, never a rectangle or frame edge), graphic well border |
| `track` | `#EFEFEF` | Bar track behind a progress bar |
| `cardBorder` | `#EAEAEA` | Border on white cards inside graphics |
| `wellBg` | `#F9F9F9` | Graphic well fill |
| `connector` | `#CBCBCB` | Vertical connector lines in the orchestration module |
| `white` | `#FFFFFF` | Card fills, type on gradient bars |
| `coralLight` | `#FCA694` | Coral gradient start |
| `coral` | `#F6816A` | Coral gradient end, "at risk" status text |
| `tealLight` | `#5FBEC8` | Teal gradient start |
| `teal` | `#3FA7B7` | Teal gradient end, column label (right) |

### Brand gradient (4 stop)

Used for the page 1 hero glow and for gradient card borders. Never as a flat fill
behind prose.

```
stops: 0.10 #D8F6FF · 0.20 #9CDFF3 · 0.60 #FCE1DA · 1.00 #FF5331
hero transform:   [[-0.701, 0.009, 0.764], [0.525, -0.595, 0.466]]
card border transform: [[0.48, -0.44, 0.47], [0.27, 0.62, 0.01]]
```

## Type

Two families only. **Roboto Serif Light** for every display level. **Geist** for
everything else. No third family, no other weights of Roboto Serif.

| Role | Font | Size | Line height | Tracking | Colour |
|---|---|---|---|---|---|
| Document title | Roboto Serif Light | 72 | 112% | -0.2% | `ink` |
| Section heading | Roboto Serif Light | 40 | 124% | -0.2% | `ink` |
| Pain point headline | Roboto Serif Light | 34 | 124% | -0.2% | `ink` |
| Prose section headline | Roboto Serif Light | 32 | 124% | 0 | `ink` |
| Closing heading | Roboto Serif Light | 34 | 124% | — | `ink` |
| Stat numeral | Roboto Serif Light | 54 | 110% | -1% | `ink` |
| Graphic caption | Roboto Serif Light | 19.4 | 124% | — | `ink` |
| Numeral inside a large bar | Roboto Serif Light | 34 | — | — | `white` |
| Numeral inside a small bar | Roboto Serif Light | 26 | — | — | `white` |
| Meta line | Geist Regular | 19 | 150% | -0.2% | `body` |
| Intro paragraph | Geist Regular | 17 | 140% | -0.2% | `body` |
| Column label, situation | Geist Medium | 18 | 150% | — | `coral` |
| Column label, response | Geist Medium | 18 | 150% | — | `teal` |
| Prose, situation column | Geist Regular | 15 | 130% | -0.2% | `soft` |
| Prose, response column | Geist Regular | 15 | 130% | -0.2% | `strong` |
| Prose, section block body | Geist Regular | 15 | 140% | -0.2% | `body` |
| Value in a label/value row | Roboto Serif Light | 19.4 | 124% | — | `ink` |
| Card title in graphic | Geist Medium | 16–18 | — | — | `strong` |
| Bar row label | Geist Regular | 15 | — | — | `strong` |
| Status, at risk | Geist Regular | 14 | — | — | `coral` |
| Status, neutral | Geist Regular | 14 | — | — | `muted` |
| Caption inside a well | Geist Regular | 14 | — | — | `muted` |
| Stat label | Geist Regular | 14 | 150% | -0.2% | `muted` |
| Footer | Geist Regular | 13 | — | — | `muted` |

Body copy is never centred. Only stat columns and numerals inside bars are
centred.

## Vertical rhythm

Padding applied to the top of each content block, in order down the page.

| Block | Top padding |
|---|---|
| Header (title + meta), gap between them | 20 |
| Divider wrapper | 40 |
| Intro paragraph wrapper | 30 |
| Stat row wrapper | 48 |
| Section heading wrapper | 62 |
| Rule wrapper between comparison rows | 30 above **and** 30 below the line |
| Comparison row internal gap | 15 (response column) |
| Comparison row column gap | 107 (headline 444, response 514) |
| Graphic block inside a comparison row | 20, then 15 between caption and well |
| Prose section blocks, column itemSpacing | 30 |
| Prose section block internal gap | 12 |
| Graphic block inside a prose section | 46, then 20 between caption and well |
| Closing block | 54 |

Stat row is 695 px wide with `SPACE_BETWEEN`, not full content width. Each stat
column hugs its content, numeral over label with a 4 px gap, and the column is
centre aligned: `counterAxisAlignItems = "CENTER"` plus `textAlignHorizontal =
"CENTER"` on both texts. Hugging alone leaves them left aligned, which is wrong.

## Effects

### Coral bar

```
fill:   GRADIENT_LINEAR  0:#FCA694  1:#F6816A
radius: 10 (horizontal bars) or 12 (vertical bars, cards)
effects:
  INNER_SHADOW  color #FFFFFF @0.45  offset y1  radius 0  spread 0
  DROP_SHADOW   color #F6816A @0.60  offset y8  radius 18 spread -6
```

Vertical coral bars use `offset y12, radius 22, spread -8`.

### Teal bar

```
fill:   GRADIENT_LINEAR  0:#5FBEC8  1:#3FA7B7
radius: 10 or 12
effects:
  INNER_SHADOW  color #FFFFFF @0.40  offset y1  radius 0  spread 0
  DROP_SHADOW   color #3FA7B7 @0.55  offset y10 radius 20 spread -8
```

Gradient transform is `[[1,0,0],[0,1,0]]` for horizontal bars and
`[[0,1,0],[-1,0,1]]` for vertical bars.

### White card inside a graphic

```
fill:   #FFFFFF
stroke: #EAEAEA, 1px
radius: 10 (system cards) or 12 (metric and market cards)
effects:
  DROP_SHADOW  #000000 @0.05  offset y3  radius 6  spread 0
  DROP_SHADOW  #000000 @0.04  offset y1  radius 1  spread 0
```

### Graphic well

```
fill:   #F9F9F9
stroke: #ECECEC, 1px
radius: 22
width:  1072 (full content width)
```

Inner padding is 44 px left and right. First element sits at y 28–44 depending
on module. Caption inside the well sits at x 44 near the bottom edge.

### Page 1 hero glow

```
frame "hero" at (-100, -329), size 1440 × 684, fill #FFFFFF, clipsContent true
  rect "gradient" at (-100, 130), size 1751 × 554, opacity 0.80
        fill:   GRADIENT_LINEAR, brand 4-stop, hero transform
        effect: LAYER_BLUR blurType PROGRESSIVE, radius 0,
                startRadius 98.8, startOffset (0.5, 0), endOffset (0.5, 1)
```

The hero holds one child, the wash rectangle. The glow reads as a soft
coral-to-cyan wash across the top of the page, fading to white before the intro
paragraph. It must never sit behind body copy strongly enough to reduce
contrast.

The wash is **smooth**: one gradient, with nothing laid over the colour. A
hero built with a second layer in it is wrong.

### Landscape glow positions

The hero is built for a 1240 page, so on a 1920 canvas clone it and call
`rescale(1.5)` first. Cover slides take (-120, -500) for the full wash. Every
content slide takes **(-120, 816)**, which puts a clearly visible coloured base
along the bottom edge. Do not use a lower value: at 1000 the wash barely reads
and the slide looks like a bare white page.

### Continuation page gradient

**Every page after page 1 gets one.** It is the same `hero` node, cloned and
placed at **(-100, 1506)** instead of (-100, -329). The page clips at 1754, so
only the top 248 px of the glow shows: a soft wash rising off the bottom edge
behind the footer. Page 1 gets the full glow at the top, every following page
gets the small one at the bottom.

```
page 1:        hero clone at (-100, -329)
pages 2 and on: hero clone at (-100, 1506)
```

Insert it as the **first** child of the page frame so it sits behind everything.
Do not scale it, do not recolour it, do not skip it because the page runs light.
A multi-page Keeyu document with bare white continuation pages is wrong.

---

## Dot grid (page background)

Measured from the `Example` frame on `Doc 1 · What we heard`, 2026-08-07. That
frame is the reference: match it rather than re-deriving these.

    dot_colour        #000000 at 8% paint opacity    (not a grey hex)
    dot_radius        1.5 px
    dot_spacing       20 px, centre to centre
    tile              400 x 300, dots inset 10 px on every edge so tiles butt
    page_tile         1240 x 1754, 4 x 6 of the above

    fade_mask         alpha 0 at 0%, 0.06 at 35%, 0.225 at 70%, 0.5 at 100%
    scrim             1239 x 1736 at (1, 9), paper #FAFAFA
                      alpha 1 at the top of the page to alpha 0 at the foot

The dot colour is black at 8 percent rather than a fixed grey so the texture
multiplies onto whatever sits under it. It was 10 per cent until 2026-08-14.
The strength lives on the nested `dots` vectors inside the page component, not
on the tile, so one edit cascades to every frame that instances it.

Rendered result, measured on a 3x render down the left page margin: the darkest
dot pixel is 255 at the top of the page, 253 at the midpoint, 248 at three
quarters and 243 at the foot. It is meant to be barely there.

## Paper

    page_ground       #FAFAFA        (2026-08-07; was #FFFFFF)

Carried by the sheet, the frame, the hero's own ground rectangle, the hero's
white fade rectangle and the dot grid scrim. All four must match or an edge
appears where they meet. Cards and wells keep their own fills.


---

## Status and number chips

Measured from the approved `chip`, 2026-08-17. The chip is how a status, a track
name or a list numeral is set anywhere in the system. It is the one place a
short label is allowed to sit inside a container, because it is a token rather
than prose, and it is the only exemption to non-negotiable 1.

    frame        HORIZONTAL auto-layout, hug on both axes
    padding      4 top and bottom, 7 left and right
    radius       6
    align        counterAxisAlignItems CENTER
    fills        [ #FFFFFF solid, then the gradient painted over it ]
    text         Geist Medium 11, #FFFFFF, 130% line height, -0.2% tracking
    effect       DROP_SHADOW  base colour @0.55  offset y10  radius 20  spread -8

Three colourways. The gradient runs light stop to base stop on the identity
transform `[[1,0,0],[0,1,0]]`, and the drop shadow always takes the **base**
colour at 55 per cent so the glow matches the pill.

    teal     #5FBEC8 -> #3FA7B7    resolved, confirmed, answered
    coral    #F9A898 -> #F6816A    open, outstanding, a problem
    grey     #B4B8BD -> #9AA0A6    no state, informational

The light stop of each pair is the base colour at the same hue and saturation
with lightness raised about ten points. Derive a new colourway that way rather
than picking a tint by eye.

**Numerals need a fixed text box.** Geist has no tabular figures, so `1` sets
narrower than `2` and a column of hugging chips comes out ragged down its right
edge. Set the text node to `FIXED` width and centre it: **9** for one digit,
**15** for two. Every chip in the column is then identical.

### The large chip

List numerals use the chip at **1.3x**, every dimension scaled together:

    font 14.3    padding 5.2 / 9.1    radius 7.8
    shadow       offset y13  radius 26  spread -10.4
    result       30 x 29

Scale the shadow with it. A 1.3x pill over an unscaled glow reads as a sticker.

## Gradient border box

The treatment for a table. The table frame itself carries the border; never add
a wrapper rectangle behind it.

    strokes       brand 4-stop, card border transform
                  [[0.48,-0.44,0.47],[0.27,0.62,0.01]]
    strokeWeight  1
    radius        22
    fills         none, so the page ground and its dot grid show through
    padding       28 top and bottom, 44 left and right

The box sits inside a padding-only wrapper carrying the 30 px gap from the
heading above it. **Renarrow the columns** to `CW - 88 = 984` when you box a
table or the content collides with the border. A four-column commercial table
goes 258 / 242 / 242 / 242; a three-column checklist goes 220 / 600 / 116.
