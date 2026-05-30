# TBS Prototypes (public)

Shareable web prototypes for the turn-based-strategy project. Each prototype tests a single mechanic or UX idea in isolation. No build, no deps — open `index.html` in any browser, or visit the live URL below.

Design source-of-truth (GDD, tech spec, AI design, etc.) lives in the private `turn-based-strategy` repo. This repo only hosts the public-shareable artifacts.

## Prototypes

| Prototype | What it tests | Live |
|---|---|---|
| [tech-tree-drag](./tech-tree-drag/) | Drag-line research economy — draw from any owned tech to any target; distance = cost | [▶ Play](https://markgrossnickle.github.io/tbs-prototypes/tech-tree-drag/) |
| [hex-map-iso](./hex-map-iso/) | 12×12 hex map at slight iso angle; mobile pan + pinch zoom; 4 terrain types | [▶ Play](https://markgrossnickle.github.io/tbs-prototypes/hex-map-iso/) |

## Add another prototype

1. New folder under repo root with an `index.html` and a `README.md` describing what it tests
2. Push to main
3. GitHub Pages picks it up automatically at `markgrossnickle.github.io/tbs-prototypes/<folder>/`
