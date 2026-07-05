# 💧 interactive-metaballs

> HTML5 Canvas + SDF 기반 메타볼(Metaball) 액체 결합 시뮬레이션 — 마우스 커서로 끌어당기고, Blob끼리 자연스럽게 융합되는 고성능 2D 유체 효과

HTML5 Canvas 2D에 다수의 Blob(메타볼)을 띄우고, 각 Blob을 signed-distance-field(SDF) 합성 + 부드러운 색상 그라데이션으로 렌더링하면 서로 가까울 때 자연스럽게 융합되는 액체 효과를 얻습니다. 마우스 커서를 움직이면 가장 가까운 Blob이 끌려오고, 클릭하면 새 Blob을 분사할 수 있습니다. Web Worker로 nearest-neighbor를 분리해 메인 스레드 부하를 줄이고, 60fps로 안정 동작합니다.

[🇰🇷 한국어 (기본)](#) · [🇺🇸 English](./README.en.md)

---

## 🎬 라이브 데모 (Live Demo)

> **🛠️ 진행 중 (In Progress)** — OpenCode CLI 환경에서 [MiniMax-M3](https://example.com) 모델로 작업 예정

| | |
|---|---|
| ![Status](https://img.shields.io/badge/Status-In_Progress-F59E0B?style=flat-square) | ![Stack](https://img.shields.io/badge/Stack-Canvas_+_SDF-06B6D4?style=flat-square) |
| ![License](https://img.shields.io/badge/License-MIT-F1C40F?style=flat-square) | ![Deps](https://img.shields.io/badge/Dependencies-0-9CA3AF?style=flat-square) |

---

## 🤖 생성 정보 (Attribution)

이 프로젝트의 코드는 아래 모델과 프롬프트를 이용해 **자동으로 생성**됩니다.

| 항목 | 값 |
|---|---|
| **모델** | MiniMax-M3 |
| **실행 환경** | OpenCode CLI |
| **저장소** | [`sigco3111/interactive-metaballs`](https://github.com/sigco3111/interactive-metaballs) |
| **라이선스** | MIT |
| **의존성** | 없음 (Vanilla JS + Canvas 2D, 단일 HTML) |

### 📝 사용된 프롬프트 (원문)

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

## ✨ 주요 특징 (예정 — Features)

- 🧪 **메타볼 합성 (Metaball composition)** — SDF threshold + 부드러운 그라데이션으로 블롭 간 자연스러운 융합/분리
- 🖱️ **마우스 인터랙션** — hover 시 가장 가까운 Blob 끌어당김 + 클릭 시 새 Blob 분사
- 🌈 **풀 컬러 그라데이션** — Blob별 고유 색상 + 발광(Glow) 후처리
- ⚡ **60fps 고성능** — `requestAnimationFrame` + Web Worker로 nearest-neighbor 분리
- 📦 **단일 HTML** — 외부 의존성 0개, 파일 하나만 열면 실행

---

## 🚀 실행 방법 (Quick Start)

> ⚠️ **현재 단계**: OpenCode CLI에서 코드 자동 생성 중. 이 섹션은 배포 후 자동 갱신됩니다.

### 방법 1: 브라우저로 열기 (배포 후)
```bash
open index.html        # macOS
xdg-open index.html    # Linux
start index.html       # Windows
```

### 방법 2: 로컬 서버 (권장)
```bash
python3 -m http.server 8000
# → http://localhost:8000
```

---

## 🎮 조작법 (예정 — Controls)

| 입력 | 효과 |
|---|---|
| **마우스 이동** | 커서 주변 Blob이 부드럽게 끌어당겨짐 |
| **마우스 클릭** | 새 Blob이 클릭 위치에 분사되어 추가됨 |
| **마우스 드래그(홀드)** | 가장 가까운 Blob이 커서 방향으로 끌려옴 |
| **우클릭 / 더블클릭** | (옵션) Blob 분사 모드 / 리셋 |

---

## 🛠️ 기술 스택 (예정 — Tech Stack)

| 영역 | 사용 기술 |
|---|---|
| **렌더링** | HTML5 Canvas 2D Context + ImageData 블롭 SDF 합성 |
| **물리/모델** | 각 Blob의 signed-distance field + 부드러운 임계값 합성 |
| **마우스 입력** | `mousemove` / `mousedown` / `mouseup` + nearest-blob pick |
| **워커 분리** | Web Worker에서 nearest-blob 계산 → 메인 스레드 응답성 확보 |
| **색상** | Blob별 HSL 그라데이션 + 발광 (bloom-like) 효과 |
| **루프** | `requestAnimationFrame` |
| **의존성** | 없음 (Vanilla JS) |

---

## 📂 프로젝트 구조

```
interactive-metaballs/
├── index.html          # 단일 HTML (Canvas + SDF 합성 + 인터랙션)
├── README.md           # 한국어 (기본)
├── README.en.md        # English (옵션)
├── LICENSE             # MIT
└── .gitignore          # Node/IDE/.vercel 제외
```

---

## 🎨 디자인 결정 (예정 — Design Choices)

> OpenCode 작업 중 결정될 디자인 포인트를 이 섹션에 누적합니다.

| 결정 포인트 | 선택 | 이유 |
|---|---|---|
| | | |
| | | |
| | | |

---

## 📜 License

MIT © 2026 sigco3111

---

## 🙏 Acknowledgments

이 프로젝트는 [MiniMax-M3](https://example.com) 모델과 OpenCode CLI 환경에서 생성됩니다. 프롬프트 엔지니어링과 디자인 결정은 저장소 소유자가 직접 수행합니다.

- **코딩미션 참조 페이지**: [cokac.com — 코드깎는노인](https://cokac.com/list/announcement/24)
- **이전 미션 README 템플릿**: [sigco3111/neon-fluid](https://github.com/sigco3111/neon-fluid)
