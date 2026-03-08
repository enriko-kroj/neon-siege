# Neon Siege

> A hand-crafted, single-file arcade shooter — zero dependencies, zero frameworks, pure code.

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)
![Size](https://img.shields.io/badge/Size-~60KB-brightgreen)
![Dependencies](https://img.shields.io/badge/Dependencies-0-brightgreen)

---

## Overview

**Neon Siege** is a fully self-contained, single-file arcade shooter built from scratch using raw HTML5 Canvas, CSS, and vanilla JavaScript. No game engine. No libraries. No build tools. Every system — physics, audio, rendering, UI, and persistence — written entirely by hand.

```
Open neon-siege.html in any modern browser. That's it.
```

---

## Features

### Gameplay
- **5 enemy types** with distinct AI: Drones, Tanks, Stealth units, Rushers, and Juggernauts
- **Combo multiplier** — chain kills for exponentially higher scores
- **3 powerups** — Spread shot, Energy Shield, and Laser beam with timed duration bars
- **Gradual wave spawning** with escalating difficulty across unlimited waves
- **Rusher AI** with pre-charge warning animation and screen-clearing rush attacks

### 5 Unlockable Ships

| Ship | Speed | Fire Rate | Special |
|------|-------|-----------|---------|
| VIPER I | 5.0 | 18 | Starter |
| VIPER II | 5.6 | 15 | — |
| SPECTER | 6.2 | 13 | — |
| PHOENIX | 6.8 | 12 | Rockets (r=28) |
| TITAN | 7.4 | 10 | Rockets (r=44) |

Ships are **locked to the difficulty they were earned on** — an unlock in HARDCORE doesn't carry over to NORMAL.

### 50-Challenge Progression
Tracks kills, wave survival, score milestones, combo chains, and powerup collection. Every 10 completions unlocks the next ship tier.

### 3 Difficulty Modes
| Mode | Lives | Enemy Behaviour |
|------|-------|-----------------|
| NORMAL | 5 | Relaxed fire, loose aim |
| VETERAN | 3 | Denser fire, sharper tracking |
| HARDCORE | 1 | No mercy |

---

## Controls

| Input | Action |
|-------|--------|
| `WASD` / `Arrow Keys` | Move (bottom zone) |
| `Space` | Fire |
| `Shift` | Speed boost |
| `P` / `Escape` | Pause |

---

## Technical Highlights

### Architecture
- **Single HTML file** — the entire game including CSS, audio engine, game logic, UI, and save system in one `~60KB` file
- **Fixed-timestep game loop** — logic runs at a locked 60fps independent of monitor refresh rate (60Hz / 144Hz / 165Hz all play identically)
- **Canvas 2D API only** — every frame drawn from scratch; no sprites, no textures, no WebGL

### Procedural Audio Engine
All sound is generated at runtime using the **Web Audio API** — zero audio files loaded. The soundtrack is synthesised from sawtooth bass lines, square-wave arpeggios, and procedural percussion. Every SFX (shoot, explode, powerup, hit, rocket) is built from oscillators and noise buffers on the fly.

### Pseudo-3D Renderer
All ships and enemies are drawn on Canvas with a pseudo-3D look: shadow offsets simulate depth, linear/radial gradients create lit top-faces and shaded undersides, and bevel highlights trace silhouette edges.

### Performance Engineering
- Grid background batched into a **single draw call** (down from 30 individual `stroke()` calls)
- Stars rendered without per-element `save()`/`restore()` shadow overhead
- **Hard caps** on particle count (260) and enemy bullet count (70) to prevent accumulation lag in dense waves
- Conditional shadow blur — particles below 30% opacity skip the expensive `shadowBlur` pipeline

### Systems Design
- **Rusher timeout tracking** — `setTimeout`-spawned rushers use a `pendingRushers` counter and stored timeout IDs, preventing cross-wave contamination and zombie spawns after game-over
- **Per-difficulty ship persistence** — `localStorage` stores ship unlocks and active selections as separate objects per difficulty mode, with auto-migration from legacy save formats
- **Kill handler routing** — all enemy deaths (bullet, rocket, laser, shield contact) go through a central `killE()` function, ensuring score, combo, and all 8 challenge stat types are always correctly credited

---

## Project Stats

| Metric | Value |
|--------|-------|
| File size | ~60 KB |
| External dependencies | **0** |
| Lines of JavaScript | ~1,100 |
| Audio files | **0** (all synthesised) |
| Image assets | **0** (all Canvas-drawn) |
| Challenge objectives | 50 |
| Ship tiers | 5 |

---

## Browser Support

Works in any modern browser with Web Audio API and Canvas 2D support.
Tested on Chrome, Firefox, and Edge.

---

## Author

**Enriko Kroj**  
Computer Science Student · University of Luxembourg

> *"Everything rendered, everything synthesised, everything hand-coded."*
