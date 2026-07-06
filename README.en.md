# 💧 interactive-metaballs

> HTML5 Canvas + Raw WebGL/GLSL metaball liquid-merging simulation — drag blobs with your mouse, click to inject new ones, fused via Gaussian blur pipeline at 60fps on the GPU

A raw WebGL 1.0 context renders two passes (downsample → Gaussian blur) that accumulate signed-distance-fields from thousands of Blobs, producing smooth liquid metaballs that merge when close and split when apart — all at 60fps. Blob radii are drawn from `logNormalRadius()` for natural size variety; the nearest Blob drifts toward your cursor, and clicking spawns a new one with a logNormal-distributed radius. Every GLSL shader and the entire JS logic live embedded in a single HTML — zero external dependencies.

[🇰🇷 한국어 (기본)](./README.md) · [🇺🇸 English](#)

---

## 🎬 Live Demo

> **👉 [https://interactive-metaballs.vercel.app/](https://interactive-metaballs.vercel.app/)** — open in any modern browser (60fps, GPU acceleration recommended)

| | |
|---|---|
| ![Status](https://img.shields.io/badge/Status-Live-22C55E?style=flat-square) | ![Stack](https://img.shields.io/badge/Stack-WebGL_+_GLSL-06B6D4?style=flat-square) |
| ![Live](https://img.shields.io/badge/Live-Demo-7C3AED?style=for-the-badge&logo=vercel&logoColor=white) | [![Repo](https://img.shields.io/badge/GitHub-sigco3111%2Finteractive--metaballs-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/sigco3111/interactive-metaballs) |
| ![License](https://img.shields.io/badge/License-MIT-F1C40F?style=flat-square) | ![Deps](https://img.shields.io/badge/Dependencies-0-9CA3AF?style=flat-square) |

### 🎮 Quick controls
1. Click the link above → page opens in your browser (GPU acceleration on)
2. **Mouse move** — the nearest Blob drifts toward your cursor (spring + damp)
3. **Mouse click** — spawn a new Blob at the click position (logNormal radius)
4. Watch nearby Blobs merge smoothly via the GPU pipeline, then split when they drift apart

---

## 🤖 Attribution

This project's code is **auto-generated** using the following model and prompt.

| Field | Value |
|---|---|
| **Model** | MiniMax-M3 |
| **Environment** | OpenCode CLI |
| **Repository** | [`sigco3111/interactive-metaballs`](https://github.com/sigco3111/interactive-metaballs) |
| **License** | MIT |
| **Dependencies** | None (Vanilla JS + Raw WebGL/GLSL, single HTML) |

### 📝 Prompt Used (verbatim from source)

```
HTML5 Canvas API만을 사용하여 여러 개의 메타볼(blob)들이 서로 가까이 가면 자연스럽게
합쳐지고 멀어지면 분리되는 부드러운 2D 액체 결합 시뮬레이션을 구현해줘.
각 메타볼은 서로 다른 색상과 크기를 가지고, 마우스 커서를 움직이면 커서 주변의
메타볼이 끌어당겨지며, 마우스를 클릭하면 새로운 메타볼이 분사되어 추가되도록 해줘.
시각적으로 매혹적인 컬러풀한 액체 효과를 위해 부드러운 그라데이션과 발광(Glow) 효과를
적용하고 60프레임으로 부드럽게 동작하는 고성능 인터랙티브 애니메이션을 작성해줘.
Implementation Advice: Use HTML5 Canvas 2D rendering with metaball effect via
additive blending or SDF (signed-distance-field) thresholding. Use requestAnimationFrame
for the loop. Consider Web Workers for nearest-neighbor calculation to keep the main
thread responsive. 모든 의존관계의 코드를 하나의 HTML에 담는 형태로 코드 작성.
```

---

## ✨ Features

- 🧪 **SDF metaball composition** — fragment shader accumulates per-Blob signed-distance-field with smooth threshold
- 🌀 **Two-pass Gaussian pipeline** — downsample → blur → upsample for soft glowing boundaries
- 🎲 **`logNormalRadius` distribution** — Blob sizes follow log-normal scale (few big, many small)
- 🖱️ **Mouse interaction** — nearest Blob drifts toward cursor + click spawns new Blob
- 🌈 **Full-color gradient** — per-Blob HSL palette + glow halo
- ⚡ **60fps** — all rendering on GPU; main thread only handles input + RAF loop
- 📦 **Single HTML** — zero external dependencies; double-click to run
- 🩺 **Self-test on boot** — `runSelfTest` prints helpful diagnostics to console on context loss / shader compile failure

---

## 🚀 Quick Start

### Method 1: Live demo (Vercel) — easiest
Click the Live Demo link above → runs without any install or clone.

### Method 2: Open in browser directly
```bash
git clone https://github.com/sigco3111/interactive-metaballs.git
cd interactive-metaballs
open index.html        # macOS
xdg-open index.html    # Linux
start index.html       # Windows
```

### Method 3: Local server (recommended; better mobile compatibility)
```bash
python3 -m http.server 8000
# → http://localhost:8000
```

**GPU acceleration recommended** — WebGL works on integrated GPUs, but smooth 60fps requires a discrete GPU. Mobile is supported via `viewport-fit=cover` for fullscreen mode.

---

## 🎮 Controls

| Input | Effect |
|---|---|
| **Mouse move** | Nearest Blob drifts toward cursor (spring + damp) |
| **Mouse click (left)** | Spawn a new Blob at click (random radius, logNormal) |
| **F / B keys** | (Optional) toggle spawn-type / preset mode |
| **Resize window** | Canvas auto-resizes via `computeSize` with pixel-ratio correction |

### Console guide
- On shader compile failure or context loss, `runSelfTest` runs automatically and prints a detailed diagnostic to the console.
- Open DevTools (F12) → Console to follow `[App] ...` boot-progress logs.

---

## 🛠️ Tech Stack

| Layer | Tech |
|---|---|
| **Rendering** | Raw WebGL 1.0 (no Three.js / R3F) + Canvas 2D UI overlay |
| **Shaders** | GLSL fragment shader (`attribute vec2 a_pos` + SDF field + Gaussian blur 2-pass) |
| **Data structures** | `class App` (RAF loop), `class BlobSet` (Blob pool + logNormalRadius), `class Mouse` (event normalization) |
| **Frame buffers** | `createFBO` / `createBlurFBO` / `createDownsampleFBO` (`gl.HALF_FLOAT_OES` or `RGBA`) |
| **Mouse input** | `mousedown` / `mousemove` / `mouseup` + nearest-Blob pick |
| **Blob model** | pos + vel + radius (logNormal) + color (HSL per Blob) + soft spring + damping |
| **Loop** | `requestAnimationFrame` + fixed-dt substep |
| **Deps** | None (Vanilla JS + Raw WebGL/GLSL) |

---

## 📂 Project Structure

```
interactive-metaballs/
├── index.html          # Single HTML (WebGL shader + App/BlobSet/Mouse classes + UI)
├── README.md           # Korean (default)
├── README.en.md        # English
├── LICENSE             # MIT License
├── AGENTS.md           # OpenCode-generated project knowledge base (coding-mission context)
└── .gitignore          # Node/IDE/.vercel exclusions
```

---

## 🎨 Design Choices

Four key decisions made during brainstorming:

| Decision | Choice | Rationale |
|---|---|---|
| **Rendering backend** | Raw WebGL + GLSL (no Three.js) | Keep zero-dependency commitment while still using fragment shaders for SDF accumulation; Three.js's abstractions are nice but ~600KB minimum, too heavy for a 73KB single HTML |
| **Metaball composition** | SDF accumulation + Gaussian 2-pass | Pure additive blending yields speckly boundaries with discrete blobs; SDF accumulation + downsample/blur/upsample produces the feathery, continuous liquid halo we want |
| **Blob size distribution** | `logNormalRadius()` (log-normal) | Uniform distribution is monotone — same ratio of big to small every frame. logNormal gives many small + few large, matching real-world droplet statistics |
| **Main-thread load** | GPU shader + JS only for input/nearest | At ~10k Blobs the CPU is overwhelmed; pushing all accumulation to the fragment shader keeps mouse response snappy regardless of count |

### Customizing further

Tweak the constants near the top of `class App` / `class BlobSet` in `index.html` to dial the feel:

```js
class App {
  // Blob count
  // Blur intensity (pass count or Gaussian sigma)
  // Mouse spring strength / damping
  // Color palette (HSL hue step / saturation / lightness)
  // Threshold / smoothstep range
  // Background color (#040614 — dark navy)
}
```

For advanced users: swap the `logNormalRadius()` distribution inside `class BlobSet` for exponential or beta. Add a normal-map or reflection term inside the GLSL fragment shader for a metallic-liquid look.

---

## 📜 License

MIT © 2026 sigco3111

---

## 🙏 Acknowledgments

This project was generated by [MiniMax-M3](https://example.com) in the OpenCode CLI environment. Prompt engineering and design decisions were made by the repository owner.

- **Coding mission reference**: [cokac.com — 코드깎는노인](https://cokac.com/list/announcement/24)
- **Previous-mission README templates**: [sigco3111/neon-fluid](https://github.com/sigco3111/neon-fluid), [sigco3111/cloth-simulation](https://github.com/sigco3111/cloth-simulation)
