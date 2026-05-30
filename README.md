# Strange Equilibria · 奇异平衡 ✦

An interactive generative-art piece: a **strange attractor** — a single point governed by four constants — is iterated millions of times and rendered as the **accumulated density of its wandering**. It never repeats, never escapes. The image is not drawn; it is *deposited*, like silt from moving water.

> 一个交互式生成艺术作品。一个点,被四个常数支配,迭代上百万次——永不重复、永不逃逸;它游走的**密度**沉积成图像。换个种子,就是另一个宇宙。


![no dependencies](https://img.shields.io/badge/dependencies-p5.js%20only-1f6f63) ![reproducible](https://img.shields.io/badge/seeds-reproducible-6a9bcc) ![license](https://img.shields.io/badge/license-MIT-d97757)

<!-- Add a render: open index.html, click "↓ Download PNG", save it as docs/preview.png, then uncomment: -->
<!-- ![A render of Strange Equilibria](docs/preview.png) -->

## What makes it more than a pretty picture

- **Every seed is guaranteed alive.** Before rendering, each seed's four constants are run through a **Lyapunov-exponent test** (`assets`/inline). Only genuinely *chaotic* systems (λ > 0.45) pass; thin, collapsed, line-like attractors are silently rejected and re-rolled. So you can spin the seed dial forever and never hit a dud.
- **Density, not lines.** A point's visitation count per pixel becomes light. A per-render integer **lookup table** maps millions of accumulated hits to color in real time — faint filaments and dense caustics coexist without one drowning the other.
- **Reproducible.** The same seed always yields exactly the same universe, forever. The sidebar even shows you the equations and the Lyapunov exponent of the universe you're looking at.
- **It develops.** The attractor accumulates progressively over a couple of seconds, like a photograph surfacing in a tray.

## Try it

- **Hosted:** enable GitHub Pages (Settings → Pages → Source: *GitHub Actions*, or *Deploy from branch → main*) → live at `https://<you>.github.io/strange-equilibria/`.
- **Locally:** just open `index.html`. No build step, no server. The only dependency is p5.js from a CDN.

## Controls

| Control | What it does |
|---|---|
| **Seed** | Selects the universe (its four constants). Prev / Next / Random / type-a-number. |
| **Density** | How many millions of iterations accumulate — richness vs. speed. |
| **Contrast** | Tone curve on log-density — lifts faint filaments or deepens to stark ink. |
| **Fill** | How much of the frame the attractor occupies. |
| **Rotation** | Spins the composition. |
| **Colors** | Paper (background), Ink (filaments), Glow (dense cores). Try a dark paper + bright ink for a luminous, nebula look. |
| **Download PNG** | Saves the current 1200×1200 frame. |

## How it works

The engine is a **De Jong attractor**:

```
x′ = sin(a·y) − cos(b·x)
y′ = sin(c·x) − cos(d·y)
```

A seed deterministically picks `(a, b, c, d)` in `[-3, 3]`, gated by the Lyapunov test so the dynamics are truly chaotic. A short pre-pass measures the attractor's bounds (so it's framed well); then a single point is iterated, and each landing increments a density buffer. Density → color happens through a log-compressed, gamma-corrected lookup table for speed. Reproducibility comes from seeding p5's RNG; nothing is left to chance that shouldn't be.

The aesthetic philosophy behind the movement is in **[PHILOSOPHY.md](PHILOSOPHY.md)** — and there's a quiet idea woven into it: a strange attractor is the geometry of *bounded unpredictability* — any system that is governed but not foretold. You don't need to know that to enjoy it; you'll just feel a restless order.

## Project structure

```
strange-equilibria/
├── index.html        # the whole piece — algorithm, UI, p5.js (self-contained)
├── PHILOSOPHY.md     # the algorithmic manifesto
├── README.md
├── LICENSE
└── docs/             # (optional) put a preview.png render here
```

## Credits

Built with [p5.js](https://p5js.org/). Structure and styling follow Anthropic's algorithmic-art viewer template. Strange attractors trace back to Peter de Jong's iterated maps and the broader study of chaotic dynamical systems.

## License

[MIT](LICENSE). Make prints, fork the math, build your own universes.
