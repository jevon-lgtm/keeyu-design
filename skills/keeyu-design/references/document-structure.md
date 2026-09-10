# Keeyu Document Structure

> Section order and page rules per artefact. The Golden Set is the canonical list
> of Keeyu customer-facing documents.

## Voice

Keeyu prose is plain, specific and unhurried. It names real systems, real people
and real numbers. It does not sell inside a findings document: the "what we
heard" column states the situation without adjectives, and the "how Keeyu fixes
that" column states the mechanism, not the benefit.

- No em dashes, ever
- No exclamation marks
- Australian spelling: fulfilment, personalised, organisation, prioritise
- Numbers as written in source: `~3,500`, `16.5%`, `$48,000`
- Customer systems named exactly: Retail Directions (RMS), Shopify Plus,
  Starshipit, Zendesk, Australia Post, StarTrack, Courier Guy, Royal Mail

## What We Heard (post-Discovery)

The reference artefact. Three A4 pages.

**Page 1**
1. Hero glow, logo, title, meta line
2. Divider
3. Intro paragraph, 780 wide, naming the person interviewed and the stack
4. Stat row, four figures
5. Section heading: "Pain Points and How Keeyu Fixes Them"
6. Pain point 1, with graphic

**Page 2**
7. Pain point 2, with graphic
8. Pain point 3, with graphic

**Page 3**
9. Pain point 4, with graphic
10. Pain point 5, with graphic
11. "In short"
12. "Next step: …"

Footer reads `Discovery Call Debrief` left, `n / 3` right.

Two pain points per page is the working maximum when both carry graphics. Three
fit only if two of them are text-only.

## Other Golden Set artefacts

Same page shell, same type ramp, same graphic modules. Section order differs.

| Artefact | Stage | Format | Structure notes |
|---|---|---|---|
| What We Heard | Post-Disco | A4 portrait | As above. The reference implementation. |
| Tech Integration Brief | Post-Disco | A4 portrait | **Generic template.** Identical for every customer except the systems list. No customer name, no meta line, no date anywhere in the document. Title is always "Keeyu for Your Tech Team". |
| ROI Breakdown | Post-Disco | 1920×1080 landscape | Three-column dashboard, one page. See the dedicated section below. |
| ROI and Pricing Close Script | Post-Disco | A4 portrait | Salesperson-facing. Four beats. See the script-block recipe below. |
| The Offer | Post-Demo-Offer | 1920×1080 landscape | Two columns. No co-brand header, no meta line, title is just "The Offer". |
| Business Case | Post-Demo-Offer | A4 portrait | Longest artefact, eight sections over about eight pages. See below. |
| CS Pre-Scoping Handover | Post-Scoping | A4 portrait | Internal, table-heavy, seven pages. See below. |
| Assumptions Register | Post-Disco | Live Google Sheet | Not a PDF. A cell-state design problem. See below. |
| Disco Call Talking Track | Discovery | A4 portrait | Salesperson-facing. Five beats. Same spec as the other talking tracks. |
| CSA Post-Stage | Post-Disco or post-Demo | A4 portrait | Internal deal strategy. See below. |
| Demo Call Talking Track | Demo | A4 portrait | Salesperson-facing. Ten numbered beats, objection table, after-the-call actions. |
| Tech-MAP Call Talking Track | Post-Demo | A4 portrait | Salesperson-facing, five pages. The renamed replacement for the legacy MAP Call Track. Track B, six beats, and the economic buyer path is the core. |
| Champion Follow-Up Talk Track | Post-Demo | A4 portrait | Salesperson-facing. Four scenarios, prose only, no graphics. |
| Demo Deck | Demo call | 1920×1080 landscape, 11 slides | Screen-shared during the demo. See below. |
| Sales Agreement | Post-Tech-MAP | A4 portrait | **A design target, not frozen.** The README lists folders 01 to 13 as top priority and this is 13. See below. |

## ROI Breakdown (post-Discovery)

One landscape page, three columns, no page breaks. Use the landscape canvas
tokens. Column headings are section headings (Roboto Serif Light 40) each
followed immediately by a full-column-width rule, then an italic-free Geist
Regular 15 `soft` intro of one or two sentences.

**Column 1, "Your Confirmed Data"** — label and value rows, one per input the
customer gave during discovery, separated by rules. Order as the source gives
them. Never round or reformat a figure.

**Column 2, "The Three-Pillar Math"** — three prose section blocks, one per
pillar, headline in sentence case (`Ticket Reduction`, `Operational Efficiency`,
`Revenue Uplift`), the annual figure as a stat numeral under it, and the working
as a Geist Regular 14 `muted` line beneath. A progress-timeline graphic showing
the three pillars in proportion earns its place here.

**Column 3, "The Outcome"** — a vertical stat stack: total annual benefit,
return on investment, payback period, annual investment. Then the cost of
inaction as a quantity comparison graphic with coral bars, since it is the one
genuinely negative claim on the page.

The source PDFs set every kicker in caps: `PILLAR 1 · TICKET REDUCTION`,
`TOTAL ANNUAL BENEFIT (AUD)`, `COST OF INACTION`. **Do not reproduce those.**
They are exactly the micro-labels non-negotiable 1 bans. The words survive as
headlines and stat labels in sentence case; the caps do not.

## The talking tracks

Three artefacts share one shape: the ROI and Pricing Close Script, the Demo Call
Talking Track and the Champion Follow-Up Talk Track. All are salesperson-facing,
all are per customer, all carry a meta line. Page 1 is header, purpose as the
intro, then a label and value list of the deal facts, then the beats.

**The three-level voice** is the whole design of these documents:

- **Spoken line**, the words the rep says: Roboto Serif Light 19.4, `ink`, in
  curly quotes, 880 wide
- **Stage direction**, what to do or open: Geist Regular 15, `body`
- **Rule or warning**, what not to do: Geist Regular 15, `soft`

Beats are separated by the 30/30 rule wrapper with a Roboto Serif Light 32
headline. Number them when the source numbers them.

**Never promote stage direction to a headline.** A channel note or a duration is
direction, not a heading: at 32 serif it fights the beat title above it and the
page reads as two competing headlines. Keep it at Geist 15.

**Lists inside a beat** are one text node at 170% line height, no glyphs. The
demo tracks are full of "here is what happens" sequences and they must not turn
into bulleted slides.

**Objection tables** put the objection in the left column at Geist Regular 15
`soft` and the response in the right at Roboto Serif Light 19.4 `ink`, because
the response is a spoken line like any other.

A talking track needs at most one graphic, a progress timeline of the beats
against their durations, and only when the source gives durations. The Champion
Follow-Up has none and is correct without one.

Per artefact: the **Close Script** runs three pages, its deal facts are customer,
champion, economic buyers, tier and track, and the memory hook is a section
heading. The **Demo Call Track** runs six pages over ten numbered beats, then an
objection table, then a two-row after-the-call table splitting Keeyu actions from
customer actions. The **Champion Follow-Up** runs three pages over four
scenarios, each with a channel note, the message, and a "why it works" line in
`soft`, closing with "Never Say" and "Always Do". Set the "Never Say" lines as
spoken lines, since they are things someone would say.

## The Offer (post-Demo)

One landscape page, two columns, no meta line, no customer name in the header.
The prose names the customer; the title does not.

**Left column, about 700 wide** — "The Challenge", the pull quote, "The
Solution", "The Benefits" as prose section blocks, then a rule, then a
three-figure stat row, then the closing line "Helpdesks manage tickets. Keeyu
prevents them." at Roboto Serif Light 34.

**Right column, about 860 wide** — "Pick Your Track": a comparison table inside
a graphic well. Track names sit in teal gradient header bars with the full
skeuomorphic effect stack, attribute labels run down the left in `soft`, values
are centred in `strong`, and every row is separated by a standalone rule. Give
all three tracks the same treatment: the source does not mark one as
recommended, so neither do we. The POC footnote goes below the well in Geist
Regular 13 `muted`.

## Business Case (post-Demo)

Eight A4 pages. Longest artefact in the set. Section order:

1. Executive Summary, with the four-figure stat row on page 1, then The Problem,
   The Solution and The Benefit as prose section blocks
2. Brands We Work With, one block plus the customer pull quote
3. The Three Whys, three prose section blocks whose headlines are the claims
4. Key Pain Points, five **comparison rows** with the labels "Pain point" and
   "How Keeyu solves this"
5. The Financial Impact of Keeyu, one block plus one metric table per pillar
6. Total Financial Benefit and ROI, a three-column table, then a quantity
   comparison graphic, then Commercial Offer
7. Implementation and Support, two label and detail tables
8. Recommendation, four label and detail rows, the cost of inaction graphic, and
   Next Steps as a numbered paragraph at 170% line height

**Metric table** (sections 5 and 6): a row of three columns, metric name at 520
in Geist Regular 15 `soft`, value at 340 right-aligned in Roboto Serif Light
19.4 `ink`, status at 172 right-aligned in Geist Regular 13 `muted`. Vertical
padding 13, standalone rule between rows. No wells, no cell borders, no zebra.

## CS Pre-Scoping Handover (post-Scoping)

Internal, written for Customer Success rather than the customer, seven A4 pages.
Same shell, same ramp, same tone. The header carries the customer, the date and
the deal lead. Section order, dropping the source's numbering:

1. Order Lifecycle Tools, an orchestration graphic then a sixteen-row
   three-column table
2. Carriers by Region
3. Fulfilment Setup, a two-column table then a run-on notes paragraph
4. Critical Workflows, six **headline rows**
5. Key Stakeholders, role and person and responsibility
6. Onboarding Call Focus Areas: pain points, key objectives, what Keeyu needs
   to fix, each a prose section block
7. Commercial Context, labelled internal reference only
8. Next Steps, with a progress-timeline graphic of the dates

**Reference table**: horizontal row, vertical padding 14, `MIN` counter axis,
standalone rule between rows. First column Geist Regular 15 `soft`. Middle
column, when there are three, Geist Medium 15 `strong`. Last column Geist
Regular 15 `body`. All at 130% line height. Widths 200 / 300 / 524 for three
columns, 300 / 748 for two.

**Headline row**: the comparison row geometry with one block instead of two.
Serif 34 headline in a 444 column, a single Geist Regular 15 `body` paragraph at
130% in a 514 column, separated by the 30/30 rule wrapper. Use it wherever a
named thing needs a paragraph of explanation and there is no situation-versus-
response split to make.

**Run-on lists**: where the source uses bullets, set them as one text node with
newlines at 170% line height. No bullet glyphs, no numbers unless the source
numbers them. The leading does the separating.

## Demo Deck (demo call)

Eleven 1920×1080 slides, screen-shared live. The exemplar PDF renders A4
portrait, but the README specifies 16:9 landscape and that is what the use case
demands, so build it landscape.

The reference exemplar runs twelve slides, but the built deck runs **eleven**: the
"what we learnt" and "how we fix that" slides merge into one paired-columns
slide. Treat twelve as the source's count, not a target.

The cover and the closer are the same slide: the positioning line at Roboto Serif
Light 72 on two lines, the full hero glow at (-120, -500) after a 1.5 rescale,
and nothing else. Slides 2 to 11 take the small bottom glow at (-120, 1000).

Recurring slide layouts, all starting at (120, 140):

- **Three-up**: section heading, rule, three 520 columns of headline 32 over
  body 15. Used for the executive summary and the three whys.
- **Title left, list right**: the approved layout for any slide that enumerates
  four things. Used for what we learnt, how we fix it, and what we showed you.
  No rule anywhere on the slide.
  - Title: plain text on the frame at (120, 140), Roboto Serif Light 54,
    line height 124%, tracking -0.2%, **fixed width 833** so it wraps inside the
    left column instead of running under the list.
  - List: a vertical auto-layout at **(1013, 140), width 740, itemSpacing 52**,
    holding four items. Each item is a vertical auto-layout, width 740, gap 10:
    a `coral` Geist Medium 19 numeral at 150%, a Roboto Serif Light 44 headline
    at 124%, then a filled wrapper holding Geist Regular 20 `body` at 140%.
  - The list lands at y 936 with four items. That is the slide's natural height;
    do not redistribute it.

  The left column stays empty below the title. That asymmetry is the layout, not
  an unfinished slide, and it is the one deck layout exempt from the fill rule.

- **Paired columns**: the denser form, and the right answer whenever two lists
  are the mirror of each other. Two titles, two lists, one vertical divider.
  - Left title at (120, 140) and right title at (1071, 140), Roboto Serif
    Light 54, each wrapping inside its own column.
  - Two `items` stacks at (120, 306) and (1071, 306), **width 592, gap 30**.
    Each item is a vertical auto-layout, gap 8, holding a Geist Medium 19
    numeral, a serif headline, then Geist Regular `body`.
  - **Left numerals are `coral`, right numerals are `tealLight` `#5FBEC8`.**
    The colour is the argument: coral names the problems, teal names the fixes,
    and the reader gets the pairing without a word of explanation.
  - A vertical `rule` line between the columns, at x 883, running 616 from
    y 323. Rotate a `LINE`; do not use a thin rectangle.

## Email attachment decks (folder 08)

Four artefacts sit outside the Golden Set in `08_Email_Attachment_PDFs`, and the
README lists the folder as a design target needing visual consistency with
folder 01. Three are decks, one is an A4 guide. Two pairs are byte-identical
duplicates under different names, so there are four unique artefacts, not six.

They are **generic**, not per customer: no meta line, no customer name, no deal
facts. Otherwise they use the Demo Deck spec exactly, including the deck scale,
the glow positions and the layouts.

**Sales Deck Outline**, the top-of-funnel deck: thirteen source slides rebuilt as
**eight**. The source is a slide-per-thought deck, which produces exactly the
sparse slides the density rule forbids, so the rebuild pairs aggressively:

1. Cover
2. The reactive-operations problem: the headline beside a 2 × 2 grid of the four
   pain lines, then a full-width band, how teams handle post-purchase today, in
   three ruled columns. Seven items on one page
3. What the solution would do (5 ruled items) beside why we built Keeyu, the
   definition paragraph and the customer promise under a rule
4. How Keeyu works: detect / decide / fix, three product cards with captions
5. Fix issues before customers notice: headline and the blind-spots line in the
   left column, the five things Keeyu catches in the middle column under a
   demoted 40 pt head, the dashboard on the right. Three columns, five items
6. Works with your stack: the systems graphic on the left, built to fit your
   operation (5 items) on the right
7. Proven with brands: the logo band, four stats, the customer quote card
8. Closer over the demo call: the closing statement full width at the top, then
   a rule, then the demo-call block beside the brand tile

Every merge here follows the mirror test: problem beside how it is handled,
wish-list beside the answer, capability beside the call to action.

When two merged blocks each carry a display head, **demote the second one one
step** (54 → 40). Two 54 pt serif heads side by side on the same slide read as
two competing slides jammed together, not as one dense slide.

**Proactive Automation**, the brand deck: thirteen source slides rebuilt as
**nine**. Cover; twenty years of reactive customer service with the anxiety
quote and the three status-quo columns; built to manage problems not prevent
them, beside the seven-step manual workflow; we don't manage tickets, with
detect / resolve / prevent and the two resolution modes; every step every order
in real time, carried by the order-journey card row; the lost-in-transit
comparison, seven steps against six; the five success metrics; Keeyu augments
your team with the quote and the three founders; the market case and the close.

**Sales Promises**, the promise deck: twelve source slides rebuilt as **ten**.
Cover; brands we serve; the problem, merging the hospital-ER analogy, the buried
CX team and the three by-the-time-it's-a-ticket columns; the order-journey
orchestration graphic across nine systems; before and after; twenty promises at
risk in a four-column register; sixteen more; the EHP Labs numbers and quote;
the positioning matrix; the close.

Both source decks lean on caps eyebrows (`THE PROBLEM`, `ROOT CAUSE`,
`CUSTOM WORKFLOWS`) and on full-bleed dark slides. **Neither survives the
rebuild.** Non-negotiable 1 kills the eyebrows and the Keeyu page is white. The
information the eyebrow carried belongs in the slide title.

## Increasing information density

Two consecutive slides that mirror each other, a list of problems then a list of
fixes, four things we learnt then four things we showed, are one slide. Merge
them into paired columns. The audience sees the mapping instead of holding the
first list in memory while the second one plays, and the deck loses a slide it
did not need.

The test is whether the two lists are **item-for-item parallel**. If item 3 on
the left is answered by item 3 on the right, merge. If the lists are merely
adjacent in the source, leave them apart.

This applies beyond the deck. Wherever the system already pairs a situation with
a response, prefer the paired form over two sequential blocks:

- the comparison row, which pairs on one line
- paired columns on a slide, which pair a whole list
- before and after on the case study slide

When merging, renumber every page or slide footer and re-lay the frames on their
pitch. A deck with a hole in its numbering reads as a mistake, and it is one.
- **Before and after**: two 800 columns, `coral` label left and `teal` label
  right, a serif 19.4 quote under each, then label and value rows.

**Density is a content decision, not a spacing decision.** A slide looks full
because it carries enough, not because the gaps were stretched. Get this right
before touching a single padding value:

- **Six to eight content items per slide**, not three or four. A slide with
  three short columns and 400 px of white below it cannot be rescued by
  spacing, and trying will only open a void.
- **Two full columns as the default**, each 780 wide at x 120 and x 1020, with
  a vertical `rule` between them at x 950. This is the layout the approved
  Demo Deck slide uses, and it is the densest thing in the system.
- **Every item earns three levels**: a Geist Medium 19 label in `coral` or
  `teal`, a Roboto Serif Light 34 headline, and a Geist Regular 20 `body` line.
  Label plus headline alone leaves a slide airy; the body line is what makes it
  read as substantial.
- **A rule between every item.** Rules are what make a column read as a
  structured list rather than floating text.
- **Merge upstream.** If a source slide carries only three or four items, it is
  half a slide. Pair it with the slide beside it.

Only once the slide carries enough content, tune the fit:

1. **Slides with repeating items**: absorb the remaining height into each
   item's own top and bottom padding until the column lands near y 960.
2. **Slides with no repeating items**, such as a graphic slide, are genuinely
   short. **Centre the column vertically** between y 140 and y 1000.

**Never inflate the gaps between blocks to reach the target.** That opens a void
between the heading and the content and looks worse than the sparse slide it was
meant to fix. Only item padding or the column's y position moves.

The cover and closer are the exception. They carry one line at 96 and nothing
else, and the empty canvas is the point.

Each column also carries a `coral` Geist Medium 19 label above its headline:
`01` through `04` on the four-ups, and the source's own labels elsewhere
(`Why change`, `Why now`, `Why Keeyu`). These are the one legitimate use of a
short label in the system, because they carry the source's own structure. Set
them in sentence case, never the source's caps.

The deck uses its own type scale. See "Deck scale" in `design-tokens.md`.

## Sales Agreement (post-Tech-MAP)

The README calls this a design target with a distinct legal lineage, currently
rendered as uniform 9 pt Calibri. The design work is applying the Keeyu system
to legal structure, not restyling the legal language, and not retyping all
sixteen pages. Five pages carry the whole system:

1. Cover: title, meta line, the positioning line at serif 34, the preamble, then
   the parties and plan as schedule rows
2. Subscription fees: the three-track comparison as a four-column table with
   `teal` Geist Medium 15 headers, then fee detail as schedule rows
3. Implementation, responsibilities and payment terms as schedule rows
4. A clause specimen showing the numbering hierarchy, plus jurisdiction
5. **The Mutual Action Plan section**: confirmed tech stack, outstanding
   actions, and milestones. This is where the retired MAP PDF now lives, so the
   agreement is incomplete without it. Status values are Geist Medium and
   right-aligned, `coral` for Open and `teal` for Confirmed, so an unfinished
   row is visible at a glance.
6. Definitions, then the execution block

**Schedule row**: horizontal, vertical padding 18, term at 240 in Geist Medium 15
`strong`, meaning at 788 in Geist Regular 15 `body` at 150%, rule between rows.

**Clause**: horizontal, gap 26, the number in a 64 gutter in Geist Medium 15
`teal`, then an 880 column holding a Geist Medium 15 `strong` clause title over
Geist Regular 15 `body` at 150%. Clause spacing 16.

**Execution block**: two 504 columns, each an entity name in Geist Medium 15,
74 px of clear space, a signature rule, the name and title in Geist Regular 14
`muted`, then 44 px, a date rule, and the word Date.

Legal body copy runs at 150% line height, not the 140% used elsewhere. Contracts
are read slowly and in full.

## CSA Post-Stage (post-Discovery or post-Demo)

Internal deal strategy, three A4 pages, one per deal stage. Never sent to the
customer: the footer reads `Current Situation Analysis · Internal, not for
distribution`.

1. Header, the objective as the intro, a four-figure stat row (close
   probability, monthly price, ROI, payback), then the deal snapshot as
   label-and-value rows
2. Close probability, then the situation analysis as two columns, `teal`
   "Strengths" against `coral` "Weaknesses and threats", then the path to close
   with a stage-sequence graphic
3. The three action phases: immediate, pre-meeting, and post-meeting scenarios

**Action table**: priority number in a 44 gutter in `coral` Geist Medium 15, the
action at 320 in Geist Medium 15 `strong`, the rationale at 636 in Geist
Regular 15 `body`.

**Scenario blocks** use a traffic light the source already implies. Do not draw
coloured dots: set the scenario name in `teal` for green, `tealLight` for
yellow, `coral` for red, and let the type carry it.

**Stage sequence graphic**: the stages as white cards in a row with 2 px
`connector` links between them, the current stage filled with the teal gradient
and white type. It is the systems graphic's vocabulary turned into a timeline.

## Assumptions Register (post-Discovery)

A live Google Sheet since 28 May 2026, so the deliverable is a **design proposal
for the Sheet**, built as two landscape pages. The problem is not page layout,
it is cell state: the customer must see at a glance which numbers they own,
which came from discovery, and which are calculated.

Three cell states, mapped onto the brand rule:

- **Yours to fill**: coral tint `#FEF2EF`, labelled in `coral`. Empty until the
  customer supplies it.
- **Confirmed in discovery**: teal tint `#ECF7F9`, labelled in `teal`. Keeyu
  pre-filled it and the customer may correct it.
- **Calculated**: `wellBg`, Geist Medium, `strong`, locked.

Sheet rendering: header band 56, row height 52, first column widest, one rule
between rows and one between columns, never a full grid. **Never colour a whole
row.** Colour marks ownership of a value, so it belongs on the cell.

Page 2 documents the five tabs (Inputs, ROI Math, Pricing Scenarios, Pain
Points, Notes) and the rules for a live document: no hero glow, no header block,
no footer, because a Sheet has no pages. The type ramp still holds, with Roboto
Serif Light reserved for tab titles and for the verbatim quotes on Pain Points.

## Generic versus per-customer artefacts

Before building, decide which kind of artefact this is. It changes the header.

**Per-customer artefacts** carry a meta line under the title in the form
`Customer   ·   Artefact: Month Year`. The prose names the customer, the people
interviewed, and their numbers.

- What We Heard
- ROI Breakdown
- The Offer
- Business Case
- CS Pre-Scoping Handover

**Generic artefacts** are the same document for every deal. They have **no meta
line, no customer name and no date**. The only per-customer content is a single
list, usually of systems. The header is title then straight to the subtitle.

- Tech Integration Brief — varies only in "Systems We Connect To"
- ROI and Pricing Close Script — identical for every deal

For the Tech Integration Brief specifically, the sections are, in order:
How Keeyu Connects · What You Need to Do · How Long It Takes · Systems We
Connect To · What It Does · What It Does Not Do · In short · Next step. Keep
"What It Does" and "What It Does Not Do" as two separate blocks with their own
headlines. Do not merge them into a two-column comparison: the source does not
frame them as one.

**Scope.** The Golden Set folder holds **19** artefacts, not the 17 its README
table lists. Folders 18 (Disco Call Talking Track) and 19 (CSA Post-Stage) were
added in rev 2 and appear only in the changelog at the top of that file. Audit
the folder, not the table.

Of the 19, five appear in the README's Legacy table: 05 Executive Summary, 09
Mutual Action Plan, 11 Assumptions Register PDF, 16 MAP Call Talking Track, 17
Closing Call Talking Track. Do not assume an artefact is frozen because it looks
legal or internal: that table is the only authority.

**The Legacy table redirects, it does not always freeze.** Each row names a
replacement path, and the instruction is to design the current replacement. Read
each row before concluding there is nothing to build:

| Legacy row | What it actually means |
|---|---|
| Executive Summary | Dead. The Offer replaces it. |
| Mutual Action Plan PDF | Not dead. The MAP is now a **section inside the Sales Agreement**, and that section must be built. |
| Assumptions Register PDF | Not dead. The live Sheet replaces it, and that Sheet needs a design. |
| MAP Call Talking Track | **A rename, not a retirement.** The same artefact is live as the Tech-MAP Call Talking Track and must be built. |
| Closing Call Talking Track | Dead. Its closing beat lives in the ROI and Pricing Close Script. |

So the buildable set is **fifteen**, not fourteen: the thirteen unfrozen
artefacts plus the Tech-MAP Call Talking Track, with the MAP as a section of the
Sales Agreement rather than a document of its own.

Legacy artefacts are frozen and must not be redesigned: Mutual Action Plan PDF,
Assumptions Register PDF, MAP Call Talking Track, Closing Call Talking Track,
and the old Executive Summary. Their replacements are the Sales Agreement MAP
section, the live Assumptions Register Sheet, and The Offer.

## Choosing graphics per artefact

| Claim shape | Module |
|---|---|
| Several things at different completion states | Progress timeline |
| One layer above many systems | Systems we connect to (standardised, clone it) |
| A count going down, or a before/after quantity | Quantity comparison |
| A small set now measured or included | Metric cards |
| Parallel entities with attributes | Attribute cards |

If a claim does not fit one of these, leave it as prose. Do not invent a sixth
module type without agreeing it first: the five exist so the whole library reads
as one system.

## Page break rules

- Never split a pain point across pages
- Never leave a headline at the foot of a page with its prose overleaf
- Never split a graphic from its caption
- Content must clear y 1696
- If a page runs light, let it. White space at the foot of a page is correct;
  padding it with a graphic that does not earn its place is not.
