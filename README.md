# Chandra Kiran Teja: AI Engineer Portfolio (v2)

Personal portfolio site: computer vision, deep learning, and real-time video understanding.

Single-page, self-contained (`index.html`), no build step and no dependencies.
Fonts are self-hosted, so no visitor IP reaches a third party.

**v1 (currently live):** https://ckteja.github.io/Portfolio/ — source in `../website`, untouched.

## What changed in v2

The v1 page ran roughly 8,500px in a single key: every section computed to
`background: rgba(0,0,0,0)`, so the whole document was `#0C0D0F` from masthead
to footer. v2 keeps the structure, the copy and the live detector, and changes
how loudly the page speaks.

- **Three section grounds.** `data-key="lit"` (bone) on About, Research and
  Experience; `data-key="flood"` (full-bleed amber) on Contact, used exactly
  once. Each key only redefines the existing CSS custom properties, so every
  component inside re-themes with no rules of its own.

  The rule is semantic, not decorative: **lit is for documents** (the bio, the
  papers, the CV) and **ground is for systems** (the venture, the live demo,
  the project work, the tooling). That also gives the page its rhythm —
  dark, lit, dark, lit, then a dark run through demo/work/skills, lit, flood.

- **Publications set as a reprint.** On the lit key the three IEEE papers get a
  display numeral in the margin, the title at 1.32rem, the venue stamped in
  mono, and his own name picked out of the author list in `--ink`.
- **Display scale.** `h1` moved from `clamp(2.75rem, 6vw, 4.5rem)` at `line-height: 1.01`
  to `clamp(2.9rem, 8.4vw, 6.6rem)` at `0.9`, and out of the two-column grid into
  its own full-measure row so it holds two lines instead of breaking into four.
  Emphasis is set in italic amber (`h1 em`).
- **Proof first.** The three figures (3× IEEE, 90% on Jetson Nano, M.Sc. Passau)
  are set in display type rather than 13px mono.
- **Projects as detections.** Each `.proj` is drawn as a bounding box with corner
  ticks and a class-label tab carrying a real figure, the way his own models draw
  them. Labels encode the kind of work: `FULL-STACK`, `RESEARCH`, `EDGE-DEPLOY`.
- **i-Brick instrument.** The venture's 0–100 risk score as a dial, including the
  dashed `UNASSESSED` chip — the system's own refusal to report unmeasured as fine.

- **Skills as claim and citation.** Each group already named the work it came
  from, in links, set in the smallest and dimmest type on the page. Those cite
  lines are now marked as citations (a `USED IN` rule, links underlined in
  `--box`), and the two groups with nothing to cite — languages, tools — drop
  out of the grid into a compact row, because "Python, C, C++, SQL" should not
  hold the same weight as a group backed by three IEEE papers.

Mint (`--box`) means one thing throughout: this points at real work. It frames
the project cards, underlines the skill citations and frames the case-study
`.meta` block, and nothing else uses it.

### The case-study pages

`densenet-transformer.html`, `edge-detection.html`, `few-shot-object-counter.html`
and `404.html` are on the same system: new `--ground`, the display headline scale
(h1 to `clamp(2.4rem, 6.4vw, 4.4rem)` at `0.94`), and the `--box` tokens.

Each case study's `.meta` block is framed as a detection and carries **the same
class label as the card that links to it** — click `RESEARCH · 0.9375 UCF-101`
on the index and the page you land on repeats it, so the card and the page read
as one object.

They stay on the dark ground rather than taking the lit key. They are full of
architecture diagrams, figures and measurement tables, which read better there,
and keeping them dark makes them continuous with the Work section they open from.

Two fixes went in alongside:

- `.at` / `.at-s` / `.at-a` set the SVG diagram text with hardcoded light hex
  (`#EDEBE6`, `#A49F94`). They now take `--ink` / `--muted` / `--sig`. Nothing
  rendered wrongly before, but any non-dark ground would have made every
  architecture diagram vanish.
- The "Animal intrusion detection on edge hardware" card linked only to GitHub,
  even though `edge-detection.html` is that project's case study. It now links
  to both.
- **One orchestrated opening.** The headline wipes up from a mask on load, as a
  pure CSS animation so it can never be left invisible by a script failure, and
  the eyebrow resolves out of noise once. Everything below keeps the existing
  `IntersectionObserver` fade-ups. Both respect `prefers-reduced-motion`, and
  the eyebrow's real text is in the markup, so with JS off it is simply there.

The live detector stays at section 04 rather than moving into the masthead.
The hero frame's boxes are hand-drawn and the demo says so — "The boxes on my
portrait are drawn by hand. These aren't." Collapsing the two would cost that.

Typeface is still self-hosted Newsreader. Fraunces was considered for the display
role and is a drop-in swap (`--f-display`) if more character is wanted later.

## Local preview

Open `index.html` directly, or serve it so the scripts run:

```
python -m http.server 8787
```

## Deploying

`.github/workflows/static.yml` publishes the repository root to GitHub Pages on
push to `main`. It is carried over from v1 and will deploy wherever this repo is
pointed — check the remote before pushing.
