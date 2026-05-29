# JavaScript Tetris — Adaptive

A responsive, dependency-free HTML5 Tetris game that scales to any screen size. Forked from [jakesgordon/javascript-tetris](https://github.com/jakesgordon/javascript-tetris) with adaptive layout improvements.

**[Play the original](https://jakesgordon.com/games/tetris/) · [Original blog post](https://jakesgordon.com/writing/javascript-tetris/) · [Original source](https://github.com/jakesgordon/javascript-tetris)**

---

## Features

- **Zero dependencies** — pure vanilla JavaScript, no build tools, no npm
- **Adaptive layout** — 7 responsive breakpoints (250 px → 850 px wide) so the game fits any viewport
- **Smooth game loop** — uses `requestAnimationFrame` with a `setTimeout` fallback for older browsers
- **Performance overlay** — live FPS / frame-time / memory display via `stats.js`
- **Fair randomization** — "bag" system (4 of each piece type per shuffle cycle) prevents streaks

---

## Getting Started

No installation required. Open `index.html` directly in a browser:

```
open index.html          # macOS
start index.html         # Windows
xdg-open index.html      # Linux
```

Or serve with any static file server:

```bash
npx serve .
python -m http.server 8080
```

**Supported browsers:** Chrome, Firefox, Safari, Opera, IE 9+

---

## Controls

| Key | Action |
|-----|--------|
| `Space` | Start new game |
| `←` / `→` | Move piece left / right |
| `↑` | Rotate piece |
| `↓` | Soft drop (accelerated fall) |
| `Esc` | End current game |

---

## Scoring

| Lines cleared | Points |
|---------------|--------|
| 1 | 100 |
| 2 | 200 |
| 3 | 400 |
| 4 (Tetris) | 800 |

Each piece that locks in place adds **+10 points**. Speed increases by 0.005 s per row cleared, starting at 0.6 s/drop and capping at 0.1 s/drop.

---

## Project Structure

```
javascript-tetris-adaptive/
├── index.html      # Complete game — layout, styles, and all game logic
├── stats.js        # Third-party FPS/MS/MB performance monitor
├── texture.jpg     # Canvas background texture
├── LICENSE         # MIT
└── README.md
```

All game logic lives in `index.html` as inline JavaScript (~400 lines). There is no build step and no separate module files.

---

## Adaptive Layout

The game uses CSS media queries to rescale the block size across 7 breakpoints:

| Viewport width | Block size | Font size |
|---------------|------------|-----------|
| ≤ 250 px | 10 px | 0.75 em |
| ≤ 350 px | 15 px | 1.00 em |
| ≤ 450 px | 20 px | 1.25 em |
| ≤ 550 px | 25 px | 1.50 em |
| ≤ 650 px | 30 px | 1.75 em |
| ≤ 750 px | 35 px | 2.00 em |
| > 750 px | 40 px | 2.25 em |

The canvas (10 × 20 blocks) and the upcoming-piece preview (5 × 5 blocks) resize automatically to match the active breakpoint.

---

## Game Constants

| Constant | Value |
|----------|-------|
| Court width | 10 blocks |
| Court height | 20 blocks |
| Preview area | 5 × 5 blocks |
| Pieces | I, J, L, O, S, T, Z |
| Initial drop speed | 0.6 s |
| Minimum drop speed | 0.1 s |
| Speed increment | −0.005 s per row |

Piece rotation states are encoded as 16-bit hex masks. Each piece has 4 rotation states stored as an array of 4 values (some pieces have fewer unique rotations due to symmetry).

---

## Piece Colors

| Piece | Color |
|-------|-------|
| I | Cyan |
| J | Blue |
| L | Orange |
| O | Yellow |
| S | Green |
| T | Purple |
| Z | Red |

---

## License

[MIT](LICENSE)
