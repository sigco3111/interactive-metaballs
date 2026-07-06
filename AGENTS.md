# PROJECT KNOWLEDGE BASE

**Generated:** 2026-07-05 23:30 UTC
**Commit:** 4f99d20
**Branch:** main

## OVERVIEW
`interactive-metaballs` — single-HTML Canvas 2D demo of SDF-based metaball liquid-merge simulation with mouse interaction. Pre-code skeleton: docs only, source generation in progress.

Stack target: **Vanilla JS + HTML5 Canvas 2D + Web Worker + `requestAnimationFrame`**. Zero npm dependencies, zero build step.

## STRUCTURE
```
interactive-metaballs/
├── index.html            # [PLANNED] Canvas + SDF composition + interactions + inline JS + inline Worker
├── README.md             # Korean (default — project convention)
├── README.en.md          # English mirror
├── LICENSE               # MIT © 2026 sigco3111
├── .gitignore            # Node/IDE + OpenCode/Codex/.codegraph/.omo + .vercel (pre-block)
├── .gitkeep              # Placeholder until index.html lands
└── AGENTS.md             # This file
```

No `src/`, no `package.json`, no `node_modules/`. Single deliverable file.

## WHERE TO LOOK
| Task | Location | Notes |
|------|----------|-------|
| Project intent / prompt spec | `README.md`, `README.en.md` | Verbatim prompt is inlined under "사용된 프롬프트" / "Prompt Used" |
| Run the demo | `index.html` (when present) | `open index.html` or `python3 -m http.server 8000` |
| License terms | `LICENSE` | MIT |
| Ignore rules / mission patterns | `.gitignore` | `.codegraph/`, `.omo/`, `.vercel/`, `.playwright-mcp/` explicitly blocked |

## CONVENTIONS (this project)

- **Bilingual README, Korean first** — `README.md` is Korean (default), `README.en.md` is English mirror. Keep both in sync; Korean version ships first.
- **Single-HTML constraint** — all HTML + CSS + JS + Web Worker code lives in one `index.html`. Per the embedded prompt: *"모든 의존관계의 코드를 하나의 HTML에 담는 형태로 코드 작성"*. Do NOT split into `app.js` / `style.css` / `worker.js`.
- **Zero dependencies** — no `package.json`, no npm, no bundler. Pure browser primitives only.
- **Coding-mission v3.5 lineage** — repo follows the template from `sigco3111/neon-fluid`. `.gitignore` pre-blocks `.vercel/` to prevent OpenCode auto-modify (mission pattern).

## ANTI-PATTERNS (this project)

- **DO NOT** introduce `package.json` / `node_modules` / build tooling. The deliverable is one HTML file.
- **DO NOT** split source across multiple files. Inline everything in `index.html`.
- **DO NOT** add third-party libraries (no Three.js, no Pixi, no GSAP). Vanilla JS only.
- **DO NOT** commit `.codegraph/`, `.omo/`, `.playwright-mcp/`, `.vercel/` directories — already in `.gitignore` for a reason.
- **DO NOT** drop the Korean README or change its default status. Bilingual is the convention.
- **DO NOT** remove `.gitkeep` until `index.html` is committed.

## UNIQUE STYLES

- **Embedded verbatim prompt** in both READMEs — preserves generation provenance. Update both READMEs together if the source prompt changes.
- **Pre-emptive `.vercel/` ignore** — mission pattern from `sigco3111/neon-fluid`; prevents accidental deploy scaffolding.
- **Auto-generated attribution block** — every README has a model/environment/repository attribution table. Keep it intact; it's a requirement of the mission.
- **OpenCode-native** — `.omo/`, `.codegraph/` symlinks are expected to be present during dev and are gitignored.

## COMMANDS
```bash
# Serve locally (recommended — Worker needs http://)
python3 -m http.server 8000
# → http://localhost:8000

# Open directly in browser (fallback — Worker may not work on file://)
open index.html        # macOS
xdg-open index.html    # Linux
start index.html       # Windows
```

No build, no test, no lint commands exist yet.

## NOTES

- **Project state**: skeleton. `index.html` does not exist; code generation is in progress under MiniMax-M3 in OpenCode CLI. Once `index.html` lands, regenerate `AGENTS.md` to add the CODE MAP section (LSP/codegraph will index it).
- **Bilingual sync**: when updating `README.md`, also update `README.en.md` (and vice versa). Status badges, attribution block, and design-decision table must stay aligned.
- **Mission reference**: this repo is one in a series from `sigco3111` following the `cokac.com` coding-mission template; sibling repo `sigco3111/neon-fluid` is the previous mission and the structural template source.
- **Re-run `/init-deep`** after `index.html` is generated — it will populate the CODE MAP and may warrant a subdirectory AGENTS.md if files are split (which would violate the single-HTML rule — re-confirm).