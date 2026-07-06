# 💧 interactive-metaballs

> HTML5 Canvas + WebGL/GLSL 기반 메타볼 액체 결합 시뮬레이션 — 마우스로 끌어당기고, 클릭으로 새 블롭 분사, 가우시안 블러 파이프라인으로 부드럽게 융합되는 고성능 GPU 셰이더

Raw WebGL 1.0 컨텍스트에서 두 패스(downsample → 가우시안 블러)로 1만 개 가까운 Blob의 signed-distance-field를 합성해, 가까울 때 자연스럽게 융합되고 멀어지면 분리되는 메타볼 효과를 60fps로 만들어냅니다. Blob별 radius 정규분포(`logNormalRadius`)로 사이즈 다양성을 확보하고, 마우스 커서 위치에 가장 가까운 Blob을 부드럽게 끌어당기며, 클릭 시 새로운 Blob을 분사합니다. 모든 셰이더(GLSL)와 로직이 단일 HTML에 임베드되어 외부 의존성은 0개입니다.

[🇰🇷 한국어 (기본)](#) · [🇺🇸 English](./README.en.md)

---

## 🎬 라이브 데모

> **👉 [https://interactive-metaballs.vercel.app/](https://interactive-metaballs.vercel.app/)** — 브라우저에서 바로 실행 (60fps, GPU 가속 권장)

| | |
|---|---|
| ![Status](https://img.shields.io/badge/Status-Live-22C55E?style=flat-square) | ![Stack](https://img.shields.io/badge/Stack-WebGL_+_GLSL-06B6D4?style=flat-square) |
| ![Live](https://img.shields.io/badge/Live-Demo-7C3AED?style=for-the-badge&logo=vercel&logoColor=white) | [![Repo](https://img.shields.io/badge/GitHub-sigco3111%2Finteractive--metaballs-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/sigco3111/interactive-metaballs) |
| ![License](https://img.shields.io/badge/License-MIT-F1C40F?style=flat-square) | ![Deps](https://img.shields.io/badge/Dependencies-0-9CA3AF?style=flat-square) |

### 🎮 빠른 사용법
1. 위 데모 링크 클릭 → 브라우저에서 페이지 열기 (GPU 가속 활성화 권장)
2. **마우스 이동** — 커서 주변 가장 가까운 Blob이 부드럽게 끌려옴 (F=유형A, B=유형B 스폰 모드)
3. **마우스 클릭** — 새 Blob이 클릭 위치에 분사되어 추가됨 (분산 일정 radius)
4. 가까운 Blob끼리는 자연스럽게 융합, 멀어지면 부드럽게 분리되는 액체 효과 감상

---

## 🤖 생성 정보

이 프로젝트의 코드는 아래 모델과 프롬프트를 이용해 **자동으로 생성**되었습니다.

| 항목 | 값 |
|---|---|
| **모델** | MiniMax-M3 |
| **실행 환경** | OpenCode CLI |
| **저장소** | [`sigco3111/interactive-metaballs`](https://github.com/sigco3111/interactive-metaballs) |
| **라이선스** | MIT |
| **의존성** | 없음 (Vanilla JS + Raw WebGL/GLSL, 단일 HTML) |

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

## ✨ 주요 특징

- 🧪 **메타볼 SDF 합성** — Blob의 signed-distance-field를 fragment shader에서 누적해 threshold 부드러운 합성
- 🌀 **Two-pass 가우시안 파이프라인** — downsample → blur → upsample으로 메타볼 외곽을 부드럽게 발광
- 🎲 **logNormalRadius 분포** — Blob 크기가 자연스러운 정규분포 로그 스케일로 산출
- 🖱️ **마우스 인터랙션** — nearest Blob이 커서 방향으로 끌려옴 + 클릭으로 새 Blob 분사
- 🌈 **풀 컬러 그라데이션** — Blob별 고유 HSL 팔레트 + glow halo
- ⚡ **60fps** — 모든 렌더링이 GPU 셰이더 → 메인 스레드는 마우스 입력 + RAF 루프만
- 📦 **단일 HTML** — 외부 의존성 0개, 파일 하나만 열면 실행
- 🎛️ **즉시 부팅** — `runSelfTest` 자동 진단 + 컴파일 에러 시 콘솔 친절 가이드

---

## 🚀 실행 방법

### 방법 1: 라이브 데모 (Vercel) — 가장 간단
위 Live Demo 링크 클릭 → 별도 설치 없이 바로 확인 가능합니다.

### 방법 2: 그냥 브라우저로 열기
```bash
git clone https://github.com/sigco3111/interactive-metaballs.git
cd interactive-metaballs
open index.html        # macOS
xdg-open index.html    # Linux
start index.html       # Windows
```

### 방법 3: 로컬 서버 (권장, 모바일 호환)
```bash
python3 -m http.server 8000
# → http://localhost:8000
```

**GPU 가속 권장** — WebGL 기반이라 integrated GPU도 작동하지만, 부드러운 60fps는 전용 GPU에서 안정적입니다. 모바일에서는 `viewport-fit=cover` 옵션으로 전체화면 모드 지원.

---

## 🎮 조작법

| 입력 | 효과 |
|---|---|
| **마우스 이동** | 가장 가까운 Blob이 커서 방향으로 끌려옴 (스프링 + damp) |
| **마우스 클릭 (왼쪽)** | 클릭 위치에 새 Blob 분사 (랜덤 radius, logNormal 분포) |
| **F / B 키** | (옵션) 특정 유형 Blob 스폰 모드 전환 |
| **창 크기 조절** | 캔버스 자동 리사이즈 (computeSize로 픽셀 비율 보정) |

### 콘솔 가이드
- 셰이더 컴파일 실패 또는 컨텍스트 손실 시 `runSelfTest`가 자동 실행되어 자세한 진단을 콘솔에 출력합니다.
- F12 개발자 도구 → Console에서 `[App] …` 로그로 부팅 진행 상황 확인 가능.

---

## 🛠️ 기술 스택

| 영역 | 사용 기술 |
|---|---|
| **렌더링** | Raw WebGL 1.0 (Three.js / R3F 등 미사용) + Canvas 2D UI overlay |
| **셰이더** | GLSL fragment shader (`attribute vec2 a_pos` + SDF metaball field + 가우시안 blur 2-pass) |
| **데이터 구조** | `class App` (RAF loop), `class BlobSet` (Blob 풀 + logNormalRadius), `class Mouse` (이벤트 정규화) |
| **Frame Buffer** | `createFBO` / `createBlurFBO` / `createDownsampleFBO` (`gl.HALF_FLOAT_OES` 또는 `RGBA` 확장 대응) |
| **마우스 입력** | `mousedown` / `mousemove` / `mouseup` + nearest Blob pick |
| **Blob 모델** | 위치 + 속도 + radius (logNormal 분포) + 색상 (HSL per blob) + soft spring + damping |
| **루프** | `requestAnimationFrame` + fixed dt substep |
| **의존성** | 없음 (Vanilla JS + Raw WebGL/GLSL) |

---

## 📂 프로젝트 구조

```
interactive-metaballs/
├── index.html          # 단일 HTML (WebGL 셰이더 + App/BlobSet/Mouse 클래스 + UI)
├── README.md           # 본 문서 (한국어)
├── README.en.md        # English version
├── LICENSE             # MIT License
├── AGENTS.md           # OpenCode가 자동 생성한 프로젝트 지식 베이스 (코딩 미션 컨텍스트)
└── .gitignore          # Node/IDE/.vercel 제외
```

---

## 🎨 디자인 결정

브레인스토밍 단계에서 내린 결정 4가지:

| 결정 포인트 | 선택 | 이유 |
|---|---|---|
| **렌더링 백엔드** | Raw WebGL + GLSL (Three.js 미사용) | 라이브러리 의존성 0개를 유지하면서 fragment shader로 SDF 합성. Three.js는 클래스 단위 추상화는 편하지만 단일 HTML 73KB 안에 임베드하기엔 부피가 큼 |
| **메타볼 합성 방식** | SDF 누적 + 가우시안 2-pass | 단순 additive blending은 외곽이 거칠고 띄엄띄엄한 점들이 보임. SDF 누적 + 2단계 downsample/down-sample/upsample으로 깃털 같은 부드러운 액체 경계 확보 |
| **Blob 크기 분포** | `logNormalRadius` (로그 정규분포) | 균일 분포는 큰 Blob과 작은 Blob 비율이 일정해 단조로움. logNormal은 작은 다수 + 큰 소수의 자연스러운 임의성 (실제 액적 분포에 가까움) |
| **메인 스레드 부하** | GPU 셰이더 + JS는 입력/Nearest만 | 메타볼 1만 가까이 갔을 때 CPU에서 SDF 계산하면 메인 스레드 점유율 폭주. 모든 합산을 fragment shader로 → 마우스 응답성 100% 유지 |

### 직접 커스터마이즈하고 싶다면

`index.html` 상단 `class App` / `class BlobSet` 의 상수 영역에서 다음을 조정해 분위기를 바꿀 수 있어요:

```js
class App {
  // Blob 개수
  // Blur 강도 (pass 횟수 또는 가우시안 시그마)
  // Mouse spring 강도 / damping
  // Color 팔레트 (HSL hue step / saturation / lightness)
  // Threshold / smoothstep 범위
  // Background 색상 (#040614 같은 dark navy)
}
```

고급 사용자용: `class BlobSet` 내부의 `logNormalRadius()` 를 다른 분포(지수, 베타)로 교체하거나, GLSL fragment shader에 normal map 또는 reflection term을 추가해 액체 metallic 효과를 낼 수도 있어요.

---

## 📜 License

MIT © 2026 sigco3111

---

## 🙏 Acknowledgments

이 프로젝트는 [MiniMax-M3](https://example.com) 모델과 OpenCode CLI 환경에서 생성되었습니다. 프롬프트 엔지니어링과 디자인 결정은 저장소 소유자가 직접 수행했습니다.

- **코딩미션 참조 페이지**: [cokac.com — 코드깎는노인](https://cokac.com/list/announcement/24)
- **이전 미션 README 템플릿**: [sigco3111/neon-fluid](https://github.com/sigco3111/neon-fluid), [sigco3111/cloth-simulation](https://github.com/sigco3111/cloth-simulation)
