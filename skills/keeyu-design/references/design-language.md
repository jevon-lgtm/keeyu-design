# Keeyu Design Language

> `design-tokens.md` says **what** the values are. This file says **why**, and
> how to derive a value the tables do not list. When the two disagree,
> `design-tokens.md` wins: it is measured, this is reasoned.

Read this when you are making a judgement call. Read `design-tokens.md` when you
are looking a number up.

## Contents

1. Colour philosophy
2. Typography philosophy
3. Depth and light philosophy
4. Space and rhythm philosophy
5. Deriving values the tables do not list
6. Do's and don'ts
7. Worked prompts

---

## 1. Colour philosophy

Keeyu is **achromatic with a semantic pair**. That is the whole model.

Everything structural is grey. Five stops, and each one has a job that does not
overlap with any other stop:

| Token | Hex | Its one job |
|---|---|---|
| `ink` | `#000000` | Display type. If it is Roboto Serif, it is `ink`. |
| `strong` | `#1A1A1A` | The Keeyu response. Card titles. Bar row labels. |
| `body` | `#4D5454` | Connective prose: intro, meta, closing. |
| `soft` | `#797E82` | The customer's own words, the situation column. |
| `muted` | `#9AA0A6` | Anything the reader does not need to read: labels, captions, footer. |

The `soft` / `strong` split is doing argumentative work, not decorative work.
The situation column is set lighter than the response column because the document
is making a case: what the customer said recedes, what Keeyu will do advances.
Setting both columns at the same weight destroys the argument even though every
other value is correct.

Then there are exactly two chromatic colours, and they are **states, not
palette**:

```
coral  #F6816A (from #FCA694)   open · outstanding · a problem · the situation
teal   #3FA7B7 (from #5FBEC8)   resolved · confirmed · answered · the response
grey   #9AA0A6 (from #B4B8BD)   no state · informational
```

Three consequences follow, and they are the ones that get violated:

**Colour is never applied to prose.** A coral paragraph is not an emphatic
paragraph, it is a category error. Coral and teal appear on chips, on bars, on
column labels and on graphic objects. Never on a sentence.

**The mapping never reverses.** Teal is not "the good one" available for any
positive claim, and coral is not "the warning colour". They are the two halves of
a single before/after. Reversing them on one page of a document silently breaks
every other page.

**There is no fourth hue.** If a graphic seems to need a third or fourth
category colour, the graphic is wrong: it is trying to encode more dimensions
than the document has. Split it, or fall back to the grey chip. Do not sample a
new colour from the brand gradient to fill the gap.

### The brand gradient is not a palette

```
#D8F6FF at 0.10 · #9CDFF3 at 0.20 · #FCE1DA at 0.60 · #FF5331 at 1.00
```

These four stops exist to be rendered as light, at low opacity, behind a blur, or
as a one-pixel border. They are not colours you may pull individually and use as
fills. `#FF5331` in particular is not "the Keeyu red" and must never appear as a
solid: it is the terminal stop of a wash that is 80 percent opaque under a
progressive blur, and at full strength it does not belong to the system.

---

## 2. Typography philosophy

### Two families, and the split is semantic

**Roboto Serif Light** carries every display level. **Geist** carries everything
operational. This is not a decorative pairing; the two families mean different
things:

- Serif = *the claim*. Titles, section headings, pain headlines, graphic
  captions, stat numerals, values in a label/value row. Anything the reader is
  meant to stop on.
- Sans = *the support*. Body prose, labels, meta, statuses, footers. Anything the
  reader moves through.

A stat numeral is serif and its label is sans, on the same line, for exactly this
reason. Setting the numeral in Geist to "match the label" collapses the
distinction the whole system rests on.

### One weight of the serif

Roboto Serif appears in **Light only**, at every size from 72 down to 19.4. There
is no Regular, no Medium, no Bold serif anywhere in Keeyu. A 72 px Light serif is
a print move: at that size the thin strokes read as confident rather than weak,
and adding weight to "make it stronger" makes it look like a web headline.

Geist appears in **Regular and Medium only**. Medium is reserved for column
labels, card titles and chips. There is no Geist Bold and no Geist Light.

### Hierarchy is size, never weight

The ramp is the design:

```
72    document title
40    section heading
34    pain point headline · closing heading
32    prose section headline
19.4  graphic caption · label/value value
15    body prose
```

Between 72 and 40 is a ratio of 1.8. Between 40 and 34 is 1.18. The ramp is
deliberately top-heavy: the gaps are enormous at the top and small at the bottom,
so the page has one unmistakable entry point and then a quiet, even field. A
flattened ramp, for instance 48 / 36 / 30, is technically a hierarchy and reads
as a template.

This is why **a page that runs long breaks to a new page and never shrinks its
type**. Losing two points off the body to save a break costs more than the break
does.

### Negative tracking, and why it is small

Almost everything sets at `-0.2%`. Stat numerals set at `-1%`. That is far
gentler than the aggressive display tracking used by screen-first systems, and
deliberately so: Keeyu documents are print artefacts read at A4, where tight
tracking closes counters and hurts legibility. The tightening is there to remove
the slight looseness Roboto Serif Light has at large sizes, not to create
density.

Body copy is never centred. Only stat columns, and numerals set inside a bar, are
centred.

---

## 3. Depth and light philosophy

Keeyu has two kinds of surface, and they behave in opposite ways.

**The page is flat.** Paper, dot grid, type, hairlines. Nothing on the page
proper casts a shadow, has a radius, or sits in a container. The prose layer is
completely flat by design, which is what gives the graphics somewhere to be.

**The graphics are physical.** Every coloured object in a Keeyu graphic is lit
and casts light. That is the skeuomorphic triad:

```
1. gradient body        light stop at 0 to base stop at 1
2. white inner shadow   #FFFFFF @ 0.40-0.45, offset y1, radius 0, spread 0
3. coloured drop shadow the object's OWN base colour @ 0.55-0.60, large blur,
                        negative spread
```

Layer 2 is a one-pixel lit edge along the top. Layer 3 is the glow the object
casts down onto the paper. Two rules follow:

**The drop shadow always takes the object's own hue.** A coral bar glows coral. A
teal chip glows teal. Never black, never a neutral grey shadow. This is what
makes the object read as emitting rather than blocking, and it is the difference
between the Keeyu look and a generic material-design card.

**The three layers scale together.** When the chip goes to 1.3x, the shadow
offset, radius and spread all go to 1.3x with it. A scaled pill over an unscaled
glow reads as a sticker.

White cards inside a graphic are the exception and use conventional neutral
shadows, because they are surfaces rather than light sources:

```
#000000 @ 0.05, offset y3, radius 6      the lift
#000000 @ 0.04, offset y1, radius 1      the contact
```

### Radius carries meaning

```
6     chip                      a token
10    horizontal bar, system card
12    vertical bar, metric card, market card
22    graphic well, gradient border box    a container
```

The two ends of the scale are the load-bearing ones: 6 says *this is a label*,
22 says *this is a region of the page*. Never use a radius above 22, and never
put a radius on anything in the prose layer.

---

## 4. Space and rhythm philosophy

**All vertical rhythm comes from per-block top padding, never from `itemSpacing`
on the content column.** The column is set to `itemSpacing 0` and each block
carries its own top padding. This is what lets any block move anywhere in the
sequence without recalculating its neighbours, and it is why a build that sets
column `itemSpacing` and then fights it with negative padding is structurally
wrong even when it looks right.

The rhythm is not a uniform scale. It is a set of measured values that encode how
much separation each junction needs:

```
20   title to meta          same block, one idea
30   between prose sections
40   above the header divider
46   prose to a graphic     a graphic needs more air than a paragraph
48   above a stat row
62   above a section heading    the largest gap in the document
```

62 above a section heading and 30 between prose sections is a 2:1 ratio, and that
ratio is the reader's map of the document. Compressing 62 to fit content on a
page erases the map.

**Separation comes from space and hairlines, in that order.** Reach for a `hair`
`LINE` only where two things genuinely need to be told apart in a scan: between
comparison rows, between list items on a deck slide, under a label/value row. Not
between every paragraph.

**Content clears y 1696 on A4 and y 960 on a deck slide.** If it does not, break.
Never shrink type or tighten leading to force a fit.

**Density is the deck's rule, not the document's.** On A4, a page that ends early
is fine. On a 1920 slide, a slide that stops at y 700 is unfinished, and the
answer is never a bigger gap: run the columns wider, set the type a step larger,
or go back to the source for the content that belongs there.

---

## 5. Deriving values the tables do not list

When you need something the spec does not name, derive it rather than inventing
it.

**A new chip colourway.** Take the base colour. Raise lightness about ten points
at the same hue and saturation to get the light stop. The drop shadow is the base
colour at 55 percent. Do not pick the light stop by eye.

**A size between two ramp steps.** There isn't one. Use the nearer existing step.
The ramp is closed.

**A deck value from an A4 value.** Multiply by 1.35, then check it against the
deck table in `design-tokens.md`, which is measured and wins. The footer does not
scale. Text columns narrow rather than widen so paragraphs still run several
lines deep: three-up goes 520 to 468 with a 138 gutter, four-up 800 to 740 with a
200 gutter.

**An HTML value from a Figma value.** Multiply by 0.6403, applied to the whole
module at once via `.fig-scale`, never to individual properties.

**A shadow for a scaled object.** Scale offset, radius and spread by the same
factor as the object.

**A column width inside the gradient border box.** The box eats 44 px of padding
each side, so the content width is `CW - 88 = 984`. Renarrow the columns to fit
984, do not let the table keep its 1072.

---

## 6. Do's and don'ts

### Do

1. **Do let the type ramp carry the hierarchy.** 72 / 40 / 34 / 32 / 15 in one
   serif at one weight. Size is the only hierarchy device in the prose layer.
2. **Do emit the brand gradient as light.** A blurred hero wash, a rising
   continuation glow, or a 1 px border. Those are the three legitimate forms.
3. **Do build all three layers of the skeuomorphic triad.** Gradient body, white
   inner shadow at y1, coloured drop shadow in the object's own hue. Always all
   three, always scaled together.
4. **Do keep colour semantic.** Coral open, teal resolved, grey informational.
   Everything else is one of the five greys.
5. **Do put the dot grid on every page,** portrait and landscape, with the scrim
   as well as the mask. It is the ground, not decoration.
6. **Do build every rule as a `LINE` node** with a 1 px `hair` stroke, in the
   auto-layout flow as its own child.
7. **Do put tokens in chips and prose in the open.** A status, track name,
   milestone or list numeral is always a chip. A sentence is never in a box.
8. **Do reproduce supplied copy verbatim.** Reformat and re-lay-out freely; do
   not rewrite, summarise, merge or tighten the words unless asked.
9. **Do break to a new page** when content will not clear the footer.
10. **Do extract graphics with `get_design_context`** and transcribe the geometry
    unchanged.

### Don't

1. **Don't set micro-labels.** No tiny uppercase letter-spaced kickers, no `01`,
   no `/path-style` slugs, no `SECTION 02`, no axis ticks, no `CLIENT:` chrome.
   Under 13 px or set in caps with tracking means delete it. The only caps in the
   system is the `KEEYU` wordmark, which is a logo asset.
2. **Don't use em dashes.** Anywhere, including layer names. Commas, full stops,
   colons, or the middle dot `·`. This is a hard brand rule.
3. **Don't put prose in a container.** No cards, wells, pills or tinted panels
   around sentences. The graphic well and the cards inside it are the only
   rounded containers in the system.
4. **Don't paint the gradient as a flat fill** behind content, and don't pull
   individual stops out of it to use as solids. `#FF5331` is not a Keeyu red.
5. **Don't ship a flat coloured rectangle.** Two of the three triad layers is a
   different effect, not a lighter one.
6. **Don't add weight to make something stronger.** Roboto Serif is Light only;
   Geist is Regular and Medium only. Emphasis is size and colour-role, not
   weight.
7. **Don't shrink type or tighten leading to force a fit.** Break the page.
8. **Don't use a 1 px rectangle or a single-edge frame stroke as a line.** There
   is no exemption anywhere in the system.
9. **Don't add what the source does not contain.** No invented headline, no meta
   line where the source has none, no customer name on a generic template. If you
   are writing a sentence that is not in the source and is not a graphic caption,
   stop.
10. **Don't set the wordmark as type.** Place `assets/keeyu-logo-black.svg`, or
    the white variant on dark grounds. Never letter-space a typeface and call it
    the logo, never redraw the star.
11. **Don't eyeball a graphic from a screenshot.** It has been rejected every
    time.
12. **Don't leave a deck slide half full.** Six or more content items, two
    columns, last element landing between y 900 and y 960.

---

## 7. Worked prompts

Five components described the way the system describes them. Use these as the
model for how much precision a Keeyu build instruction carries.

**Prompt 1: Comparison row**
> Build a two-column comparison row on the 1072 content column. Left column 444,
> gutter 107, right column 514. Left: pain point headline in Roboto Serif Light
> 34, line height 124%, tracking -0.2%, colour `ink` `#000000`. Right: a column
> label in Geist Medium 18 `teal` `#3FA7B7`, then body prose in Geist Regular 15
> at 130% tracking -0.2%, colour `strong` `#1A1A1A`, internal gap 15. No
> container on either column. Separate this row from the next with a
> padding-only wrapper carrying 30 above and 30 below a `figma.createLine()`
> full-width rule, 1 px stroke in `hair` `#ECECEC`.

**Prompt 2: Coral bar in a graphic**
> Draw a horizontal bar, corner radius 10, filled with a linear gradient from
> `#FCA694` at 0 to `#F6816A` at 1 on the identity transform
> `[[1,0,0],[0,1,0]]`. Add an inner shadow, `#FFFFFF` at 0.45, offset y1, radius
> 0, spread 0. Add a drop shadow in the bar's own base colour `#F6816A` at 0.60,
> offset y8, radius 18, spread -6. If the bar carries a numeral, set it in
> Roboto Serif Light 34, `#FFFFFF`, centred. Vertical bars use radius 12, the
> gradient transform `[[0,1,0],[-1,0,1]]`, and a drop shadow at offset y12,
> radius 22, spread -8.

**Prompt 3: Status chip**
> Build a horizontal auto-layout frame hugging on both axes, padding 4 top and
> bottom and 7 left and right, corner radius 6, `counterAxisAlignItems` CENTER.
> Fills are `#FFFFFF` solid with the colourway gradient painted over it: teal
> `#5FBEC8` to `#3FA7B7` for resolved, coral `#F9A898` to `#F6816A` for open,
> grey `#B4B8BD` to `#9AA0A6` for informational, all on the identity transform.
> Text is Geist Medium 11, `#FFFFFF`, 130% line height, -0.2% tracking. Drop
> shadow in the colourway's base colour at 0.55, offset y10, radius 20, spread
> -8. For a numeral, set the text node to FIXED width and centre it: 9 for one
> digit, 15 for two, because Geist has no tabular figures.

**Prompt 4: Graphic block inside a prose section**
> Wrapper with 46 top padding. Caption first: Roboto Serif Light 19.4 at 124%,
> colour `ink`, written as a full sentence stating the point the graphic makes.
> 20 px gap. Then the well: 1072 wide, fill `#F9F9F9`, 1 px stroke `#ECECEC`,
> corner radius 22, inner padding 44 left and right, first element at y 28 to 44.
> Any caption inside the well is Geist Regular 14 `muted` at x 44 near the bottom
> edge. White cards inside the well take fill `#FFFFFF`, 1 px `#EAEAEA`, radius
> 10 or 12, and two neutral drop shadows: `#000000` at 0.05 offset y3 radius 6,
> and `#000000` at 0.04 offset y1 radius 1.

**Prompt 5: Continuation page shell**
> Frame 1240 x 1754, fill `#FAFAFA`, `clipsContent` true. First child is a clone
> of the `hero` node placed at (-100, 1506), so only its top 248 px shows as a
> wash rising off the bottom edge behind the footer. Do not scale or recolour it.
> Then the page dot grid: `#000000` at 8 percent paint opacity, dot radius 1.5,
> 20 px pitch, with both the fade mask (alpha 0 at 0%, 0.06 at 35%, 0.225 at 70%,
> 0.5 at 100%) and the `#FAFAFA` scrim at 1239 x 1736 offset (1, 9). Logo at
> (89, 70) at 130 x 30, placed as the SVG asset. Footer at y 1696: artefact name
> left at x 84, `n / total` right-aligned at x 1036, both Geist Regular 13
> `muted`. Content column is a vertical auto-layout, 1072 wide at (84, 146),
> `itemSpacing` 0, with all rhythm carried by per-block top padding.
