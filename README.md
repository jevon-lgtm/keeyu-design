# Keeyu Design

The Keeyu design system as a Claude Code plugin. Install it once and Claude builds
customer-facing documents and decks to the approved specification, without being told
the rules each time.

Covers the Keeyu Golden Set: What We Heard, Tech Integration Brief, ROI Breakdown,
The Offer, Business Case, CS Pre-Scoping Handover, and the 1920x1080 decks.

This is a **specification, not inspiration**. Every value in
`skills/keeyu-design/references/design-tokens.md` is measured from the signed-off
reference. Do not round it, scale it, or substitute something that looks close.

---

## Two ways in

This repo feeds two different surfaces. Most people want the first one.

| | What it gives you | Who needs it |
|---|---|---|
| **Claude Code** | Claude builds Keeyu documents and decks to the spec | Everyone |
| **Claude Design** | The component library, on screen, as browsable cards | Anyone designing, plus maintainers |

---

## 1. Claude Code — install the skill

Two commands, once, per machine.

```
/plugin marketplace add jevon-lgtm/keeyu-design
```

```
/plugin install keeyu-design
```

Restart Claude Code and you are done. Nothing to point at, no paths to configure,
no GitHub login needed.

### Using it

The skill fires on its own when you ask for Keeyu work:

→ "build a Tech Integration Brief for <customer>"
→ "make this in the Keeyu style"
→ "what's the Keeyu type ramp"
→ "discovery debrief for this morning's call"

### Updating

```
/plugin update keeyu-design
```

---

## 2. Claude Design — the component library

`skills/keeyu-design/keeyu-ds-bundle/` is a ready-made Claude Design system bundle.
Twenty cards across Colour, Type, Depth, Ground, Components and Rules, each one a live
HTML preview carrying its own `@dsCard` marker so it renders as a card automatically.

This is where you go to **look** at the system. Claude Code is where you **build** with it.

### Adding it

In [claude.ai/design](https://claude.ai/design), add a design system from a GitHub repo
and give it this one:

```
https://github.com/jevon-lgtm/keeyu-design
```

The repo is public, so there is no connecting of accounts or granting of access. Point
it at the bundle directory if it asks which folder holds the components:

```
skills/keeyu-design/keeyu-ds-bundle
```

That is the whole setup. The cards, their groups, names and sizes all come from the
`@dsCard` markers already in the files.

### Keeping one copy

Add it once and read from that. If everyone spins up their own private copy, the copies
drift and the design system stops being a design system. If a value needs to change, it
changes in this repo first and flows out from here.

### Pushing a change from Claude Code (maintainers)

There is also a direct sync path if you are editing the bundle locally. Once per machine:

```
/design-login
```

Then from the repo root:

```
/design-sync
```

Point it at `skills/keeyu-design/keeyu-ds-bundle`. It diffs against the remote project
and writes component by component, never a wholesale replace. Read the plan before you
approve it.

## What is in here

```
skills/keeyu-design/
├── SKILL.md              the specification and enforcement layer
├── references/
│   ├── design-tokens.md      every measured colour, type, spacing value — source of truth
│   ├── design-language.md    the reasoning behind the values, for judgement calls
│   ├── document-structure.md the Golden Set, document by document
│   ├── components.md         the component library
│   ├── html-system.md        templates, placeholders, the render pipeline
│   ├── build-guide.md        how a document gets built end to end
│   └── worked-example.md     one document built start to finish
├── assets/               base CSS, logos, a reference document
└── keeyu-ds-bundle/      live swatches: colour, type, depth, ground, components, rules
```

Read `design-language.md` and `design-tokens.md` on every job. Where the two disagree,
`design-tokens.md` wins: it is measured, the other is reasoned.

## Contributing

The design system changes rarely and deliberately. If a value needs to move:

→ Branch, change it in `design-tokens.md` first, then anywhere it is repeated
→ Bump the version in both `.claude-plugin/plugin.json` and `.claude-plugin/marketplace.json`
→ Open a PR and tag Jevon
→ Tell the team to run `/plugin update keeyu-design`

## Known gap

`references/html-system.md` points at a `keeyu-pdf-conversion` skill for the render
toolchain (`shoot.js`, `shots2pdf.py`, `build_pdfs.sh`). That skill is not in this repo
yet. Until it is, the PDF pipeline is documented here but not shipped here.

---

Proprietary. Keeyu Pty Ltd. Internal use only — see `LICENSE`.
