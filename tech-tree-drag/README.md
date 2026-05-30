# Tech Tree — Drag-to-Research Prototype

Quick exploration prototype testing an alternative research economy for TBS. Open `index.html` in any browser — no build, no dependencies, no deps to install.

## What it's testing

A different research mechanic than Polytopia's locked `tier × cities + 4` cost:

- Player drags a line from any **owned** tech (green) to any tech they want to research.
- **Distance of the drag = cost** in stars (★). Short jump = cheap. Long jump = expensive.
- Modal pops with the cost when you release the drag; Accept or Cancel.
- Endless resources (no economy gate). The `SPENT` counter tracks what you'd have spent.
- **RESET** button returns the tree to the starting state (5 tier-1 techs owned, nothing else).

## Why this mechanic might be interesting

- Player chooses their own research path geometry, not a locked tree.
- Lets a player shortcut from Tier 1 straight to a far Tier 3 if they're willing to pay the geometric cost.
- Creates an interesting tradeoff: many small jumps (incremental, cheaper aggregate) vs one big jump (faster to the late-game tech but expensive).
- "Distance = cost" gives players an immediately intuitive sense of what their research path costs without reading a table.

## Tech tree data

Polytopia's Path-of-the-Ocean tree, verbatim:
- **Tier 1 (free at start):** Climbing, Fishing, Hunting, Organization, Riding
- **Tier 2:** 2 children per Tier-1 root (10 total: Mining, Meditation, Sailing, Whaling, Archery, Forestry, Farming, Strategy, Roads, Free Spirit)
- **Tier 3:** 1 child per Tier-2 (10 total: Smithery, Philosophy, Navigation, Aquatism, Spiritualism, Mathematics, Construction, Diplomacy, Trade, Chivalry)

## Tunables (in `index.html`)

- `costFor(fromTech, toTech)` — the cost formula. Currently `Math.max(5, Math.round(distance / 4))`. Adjust the divisor to tune cost curve.
- `RING_RADII` — how far T1/T2/T3 sit from center. Adjusting changes the "natural" cost of incremental jumps vs cross-tree shortcuts.
- `NODE_RADIUS` — hit-target size.

## Tested on

- Desktop Chrome/Safari/Firefox (mouse drag)
- Mobile Safari/Chrome (touch drag) — taps and drags both work via touch events

## Open questions for the design

- Is `distance / 4` the right cost slope?
- Does owning lots of "neighbor" techs make far-jumps cheaper (e.g., cheapest path through any owned tech, not just the drag source)?
- Should there be a cap on cost? Or a soft cap with diminishing returns?
- What's the right starting set? All 5 T1s? Just 1 chosen T1? None (player picks first free tech)?
- Does the radial layout work, or would a flat tree (tiers as columns) feel better?
