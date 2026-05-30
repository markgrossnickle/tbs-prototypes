# Hex Map — Iso Prototype

Mobile-first 12×12 hex map with pan, pinch-zoom, and a slightly isometric camera angle. Open `index.html` in any browser — no build, no dependencies.

## What it's testing

- Does the slight-iso angle (Y-shear ~0.72) read well at thumbnail / hex scale on mobile?
- Are the 4 terrain types (water / plains / trees / mountain) distinguishable at full-board zoom?
- Is the seeded generator producing maps that feel coherent (lakes connect, forests clump, edges look like coast)?
- Is pinch zoom + pan acceptable on iOS Safari and Android Chrome?

## Inputs

- **Seed input** — type any integer; deterministic regeneration.
- **Reroll** — random seed.
- **Reset view** — recenters camera at zoom 1.
- **Tap a hex** — selects it (yellow ring); hover label shows axial coords + terrain.

## Touch / mouse

- 1 finger drag = pan.
- 2 finger pinch = zoom (clamped 0.4×–3.0×, zooms around pinch center).
- Tap = select; tap empty = deselect.
- Mouse wheel = zoom (desktop fallback).

## Tunables (in `index.html`)

| Constant | What |
|---|---|
| `GRID_COLS` / `GRID_ROWS` | Board dimensions (12×12 default) |
| `HEX_SIZE` | World-pixel radius per hex (36 default) |
| `ISO_Y_SCALE` | Y-axis squash (0.72 = "slightly iso"; 1.0 = top-down; 0.5 = very iso) |
| `TILE_THICKNESS` | Pixel depth of tile side at base zoom (7 default) |
| `pickRandomPoints` counts | 3 water / 5 tree / 3 mountain center seeds |

## Map generation algorithm (current)

1. Seeded RNG (mulberry32) from input.
2. Drop N random "centers" per terrain type.
3. For each tile, compute distance to nearest center per type + a small noise term.
4. Threshold to type: water (closest <1.6), then mountain (<1.5), then trees (<1.8), else plains.
5. Edge bias: boundary tiles pulled toward water (~55%) so the map feels island-like.

The same algorithm will live in `/src/game/logic/mapgen/` in the real codebase per [doc 18 §10](../../docs/18-engineering-protocols.md#10-code-organization-locked-decisions) — deterministic and runnable in Node for server-side game creation.

## What's intentionally missing

- No fog of war (this is map gen + render, not game state).
- No units, no players.
- No rivers, no roads, no resources.
- No path-cost weighting per terrain.
- No mini-map.
- No "fairness check" between players (will live in `mapgen-v1.md`, doc 14).

## Open questions for the design

- Is 12×12 right for an early-game board, or does it feel cramped/expansive?
- Does the iso angle help readability or just add visual noise on smaller phones?
- Should water tiles render lower than land tiles (deeper into the grid) to amplify the iso effect?
- Should mountains be impassable (block movement entirely) or just costly?
