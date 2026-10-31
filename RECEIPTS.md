# Receipts — Track B, "The Passage"

**Team:** The Claudettes · **Project:** Receipts · **Track:** B (UX) · **Hackathon:** Chart the Common Wealth, The Open Accelerator × Red Hat, 31 Oct 2026

**Try it live:** https://bretkerr.github.io/mass-ai-atlas/ · **Demo video (75 s):** https://youtu.be/VRSNQxPLBDM · **Repo:** https://github.com/bretkerr/mass-ai-atlas/tree/receipts

A founder says what they need. The Atlas answers with a receipt: who's on the list,
the month a person last checked each one, and what to doubt. Doubt is shown, never hidden.

## Probe made visible

**Probe 1 — "Kendall Square: an exact pin and a guess look the same."**

- **Before (10:50, 31 Oct):** 87 of 197 entries carry `approx: true`, and the map draws them
  exactly like street addresses. Zoom to Kendall Square and nothing tells you which pins are estimates.
- **After:** approximate pins are hollow dashed rings; exact addresses stay solid dots. The legend
  explains both ("Approximate: neighbourhood only", count computed live), and the tile says
  "this pin marks Kendall Square, not the street address."

Also surfaced on screen, from this morning's numbers:

| Probe | This morning | Where it shows now |
|---|---|---|
| 4 · funders without a check size | 13 of 61 state one | "Not sorted by check size: only 13 of 61 funders state one" whenever Funding is asked for; "trust less: no check size stated" per entry |
| 5 · last checked in June | 52 entries | "Last checked by a person N months ago" per entry; every card and tile shows the month |
| 2 · no connections | 104 without their own `links` | "Not connected to any other org in the Atlas" — counts links in either direction, so fewer entries (74) are flagged than lack the field |
| 6 · coverage west of Worcester | 5 entries | "None of these are west of Worcester. That is thin coverage, not proof there's nothing there." |
| 3 · startups with no stage | 35, all startups | Not treated as a gap: "Startups aren't matched to stages: they're peers, not resources." |

All counts are computed in the browser from the same data the Atlas loads; none are typed in.

## What's in it

1. **The counter** — "I need ___" above the tabs. Type or speak (browser speech recognition, no key).
   Plain keyword rules turn the words into the directory's existing *I need…* chips and stage,
   which stay visible and editable. A thermal receipt prints the five surest matches.
2. **Receipts on every card** — "✓ Checked by a person <month> · source ↗", plus a
   "Trust less:" line only when the data gives a reason. Default sort: surest first.
3. **Compare any two** — ends with one sentence: "Trust X less: …". This is the hand-off test.
4. **Flippable map tiles** — ↻ flips to the evidence; ⤢ shows more before the drawer.
5. **★ and private notes** on any tile, shown on cards and the saved list (this browser only).
6. **Smoother trackpad zoom** — fractional zoom, faster basemap redraw, no pin glow mid-zoom.

## What it refuses to do

- **Never removes or hides an entry for doubt.** Doubtful entries carry a reason and sort lower.
  Flag, never delete.
- **Never sorts funders by check size**, because most don't state one. It says so instead.
- **Never names an organization from the founder's words.** The ask only sets filters; every
  result is a real Atlas entry with its own source.
- **Never treats an empty `stages` on a startup as missing data.**

## Merging this upstream

The hero's "Watch the 75-second overview" button and "Read the one-page brief" link
belong to the hackathon entry, not the Atlas. They live in one block marked
`SHOWCASE-ONLY` in `index.html` and **hide themselves on the-open-accelerator.com**,
so the branch can be merged and deployed as is. To remove them entirely, delete that
block, the `#videoDlg` dialog, and `initShowcase` / `initOverviewVideo`.

## Data sources

- Mass AI Atlas dataset, The Open Accelerator — the-open-accelerator.com/ecosystem (CC BY 4.0),
  via this repo's `data/*.yml`. No other data is used.
- Map: OpenStreetMap via OpenFreeMap (unchanged from the Atlas).

## Run it

```bash
npm ci && python3 -m http.server   # then open http://localhost:8000
```

Code MIT. Built with Claude.
