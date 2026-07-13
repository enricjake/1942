# 1942 — Pacific Theater Arcade Shooter

A browser-based tribute to Capcom's classic 1984 arcade game **1942**.

![1942](https://img.shields.io/badge/-1942-cc3333?style=for-the-badge&logo=arcade&logoColor=white)
![HTML5 Canvas](https://img.shields.io/badge/HTML5-Canvas-e34c26?style=for-the-badge&logo=html5&logoColor=white)
![No Dependencies](https://img.shields.io/badge/No%20Dependencies-zero%20npm-green?style=for-the-badge)

## Play

Open `index.html` in any modern browser, or play online at:
**https://enricjake.github.io/1942/**

## Controls

| Key | Action |
|-----|--------|
| Arrow Keys / WASD | Move |
| Space | Fire |
| Shift + Left/Right | **Barrel Roll** (dodge enemy bullets) |
| P | Pause |

## Features

- **Barrel Roll** — the signature 1942 dodge maneuver. Press Shift + a direction to roll through enemy fire with temporary invincibility. Has a short cooldown.
- **7 enemy flight patterns** — looping arcs, swooping dives, hovering formations, zigzag sweeps, and side approaches
- **10 wave types** that cycle and scale in difficulty
- **4 power-up types**: Speed (S), Double Shot (D), Spin Fire (*), Extra Life (L)
- **Combo system** — chain kills for score multipliers up to 10x
- **Procedural sound effects** via Web Audio API — shooting, explosions, power-ups, barrel roll
- **Pacific theater aesthetics** — ocean background, scrolling clouds, tropical islands, P-38 Lightning player plane, Japanese Zero enemies with hinomaru markings
- **High score** persistence via localStorage

## Enemy Types

| Type | HP | Points | Description |
|------|-----|--------|-------------|
| Fighter | 1 | 100 | Standard Zero, light gray with red hinomaru |
| Zigzag | 2 | 200 | Sweeps side to side |
| Formation | 1 | 150 | Flies in grid patterns |
| Bomber | 5 | 500 | Large dark green, tougher |
| Ace | 10 | 1000 | White with red wingtips, boss-tier |

## Technical Details

- Pure HTML5 Canvas + vanilla JavaScript — zero dependencies
- Single `index.html` file (~700 lines)
- Fixed timestep game loop (60 FPS)
- Web Audio API for procedural sound generation
- Works on desktop and mobile browsers

---

## Disclaimer

**This is an unofficial fan project created purely for personal enjoyment and educational purposes.**

- **1942** is a registered trademark of **Capcom Co., Ltd.**
- This project is **not affiliated with, endorsed by, sponsored by, or approved by Capcom**
- No copyright infringement is intended
- This project is **free and non-commercial** — no revenue is generated
- All game logic, graphics, and sound are **original implementations** drawn from scratch using HTML5 Canvas — no original Capcom assets, code, or sprites are used
- The game design concept (vertical scrolling WWII shooter) is attributed to Capcom's original 1984 arcade game
- This project exists solely as a personal tribute and coding exercise

If Capcom or any rights holder wishes for this project to be removed, it will be taken down immediately.

## License

This project is released for personal/educational use only. Not for commercial distribution.
