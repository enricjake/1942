# AGENTS.md

## What this repo is
A single-file browser game: `index.html` (~1100 lines) is the **entire project** — HTML, CSS, and the game in one `<script>` block. Pure HTML5 Canvas + vanilla JavaScript, **zero dependencies, no build, no tests, no package manager**. README's "~700 lines" is stale.

## How to run / verify
- Open `index.html` directly in a browser. There is no dev server, bundler, or `npm` step.
- Deployed automatically via **GitHub Pages from the `main` branch** — pushing to `main` redeploys (see git history: "redeploy after enabling pages"). No separate deploy command.
- Live URL: **https://enricjake.github.io/1942/**
- No automated tests exist. Manual play in a browser is the only verification.

## Game architecture (non-obvious)
- **Single global game loop** `gameLoop()` (index.html:1077) using a fixed-timestep accumulator at 60 FPS (TIMESTEP = 1000/60). `update()` only runs when `state === 'playing'`; `draw()` always runs.
- **State machine** (`state`): `'title'` → `'playing'` → `'paused'` / `'gameover'`.
- **Web Audio** is created lazily in `initAudio()` on the first Space press (index.html:1091) to satisfy browser autoplay-gesture rules. Do not assume audio works before a keypress.
- **High score** persists in `localStorage` under key `1942hi` (index.html:120, 815).
- Enemies/waves/bullets are plain object arrays (`enemies`, `bullets`, `powerUps`, `explosions`); 10 wave formations cycle in `spawnWave()` (index.html:668).

## Known gotchas
- **Pause bug:** `gameLoop` keeps adding `timestamp - lastTime` to `accumulator` every frame even while `paused`, but only drains it when `playing`. On unpause, the `while (accumulator >= TIMESTEP)` loop replays all the missed steps instantly (a time jump). Listed in `TASKS.md` as "Fix pause state to actually pause the game loop." Fix by resetting `accumulator`/`lastTime` on pause/resume rather than rewriting the whole loop.
- All drawing uses `Date.now()` for animation timing inside draw functions, so visuals still advance while paused.

## Open work
See `TASKS.md` for the current list (pause fix, mobile touch controls, ARIA/a11y, game save/load). Confirm an item is still open before assuming it's done.
