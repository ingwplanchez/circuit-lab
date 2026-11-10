# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

---

## 📁 Repository Overview

**01_Circuitos** — Educational portal for a 5-day intensive review of **Electric Circuits I & II** targeting **Mechatronics Engineering** students. The goal is to solidify DC/AC circuit fundamentals and transient analysis as prerequisites for **Electronics I & II** (BJT/MOSFET biasing, op-amp stages, regulated power supplies, coupling/decoupling networks).

---

## 🏗️ High-Level Architecture

```
01_Circuitos/
├── index.html              # Main interactive portal (Tailwind CDN, no build step)
├── README.md               # Navigation index, progress tracking, live demo links
├── content.md              # Official 5-day syllabus with engineering objectives
├── system_prompt.md        # Pedagogical rules, lesson template (Cornell-Kwik + IPEE)
├── task.md                 # Task tracker with checklists and progress %
├── AGENTS.md               # Agent rules (this project's constitution)
├── docs/
│   ├── day_01/             # Day 1 lessons (4/4 complete)
│   │   ├── 01_ley_de_ohm.md
│   │   ├── 02_LCK.md
│   │   ├── 03_LVK.md
│   │   └── 04_mallas.md
│   └── day_02/ ... day_05/ # Future days (directories may not exist yet)
└── apps/                   # Standalone HTML/JS simulators (zero deps)
    ├── 01_serie_paralelo/
    ├── 02_lck/
    ├── 03_lvk/
    └── 04_mallas/
```

**Key architectural decisions:**
- **Zero build toolchain** — All simulators are single-file `index.html` with inline CSS/JS, loadable via `file://` or GitHub Pages
- **Tailwind via CDN** — No `package.json`, `node_modules`, or bundler
- **Vanilla JS** — No frameworks; each simulator self-contained
- **Progressive delivery** — Agent produces **exactly one lesson per turn**, then stops for user approval (enforced by `AGENTS.md`)

---

## 📚 Core Documentation (Read These First)

| File | Purpose |
|------|---------|
| `AGENTS.md` | **Mandatory rules** — agent identity, interaction flow, lesson structure, simulator standards |
| `system_prompt.md` | Lesson template (Cornell-Kwik ficha, IPEE strategy, 3 essential formulas, ASCII diagram) |
| `content.md` | 5-day syllabus with engineering objectives per day |
| `task.md` | Living checklist — update on every lesson/simulator completion |
| `README.md` | User-facing index with live demo links (htmlpreview.github.io) |

---

## 🎯 Agent Workflow (Critical)

**From `AGENTS.md` — Non-negotiable:**

1. **One lesson per turn** — Generate a single lesson (`docs/day_XX/YY_tema.md`) + its simulator prompt
2. **Stop and await approval** — Do not continue to the next lesson
3. **Update `task.md`** — Mark checklist, adjust global progress % after each completion
4. **Verify `index.html` integration** — New simulators must be linked in the main portal

**Lesson naming convention:** `docs/day_01/01_ley_de_ohm.md`, `docs/day_01/02_LCK.md`, etc.

**Simulator naming convention:** `apps/XX_descriptive_name/index.html`

---

## 🛠️ Simulator Development Standards

**Tech stack:** HTML5 + CSS3 + Vanilla JS (single file, no external deps beyond Tailwind/Google Fonts CDN)

**UI Requirements (from `AGENTS.md` §5):**
- Dark/technical theme (slate-900/950 backgrounds, sky/emerald/indigo accents)
- Sidebar controls with sliders (realistic engineering ranges: E12/E24 values, tolerances)
- Live SVG/Canvas schematic + real-time metric panels (power bars, current/voltage readouts)
- Instant updates on slider drag — no page reload

**Code patterns used in existing simulators:**
- `window.onload` → `updateSimulation()` initial render
- `input` event listeners on all sliders → recalc + DOM update
- Power formatting helper: `formatPower(W) → "X mW" | "X.XXX W"`
- SVG schematic with color-coded components (R₁=sky, R₂=emerald, R₃=indigo)
- Responsive grid: `lg:col-span-5` controls / `lg:col-span-7` viz

---

## 📐 Lesson Structure Template (Mandatory)

Every lesson in `docs/day_XX/` **must** follow this exact structure from `system_prompt.md`:

```markdown
# 📌 Día [X] - Lección [Y]: [Título]

**Objetivo de Ingeniería / Electrónica:** [Meta técnica vinculada a Electrónica I/II]

**Agenda de Tiempo:**
* **Bloque de estudio enfocado ([Z] min):** [Desglose]

---

### 1. 🖊️ Guión Rápido de Repaso
* **Fundamentos Teóricos & Conexión Electrónica:** [...]
* **Las 3 Fórmulas Esenciales:** (LaTeX with SI units)
* **Diagrama de Análisis (ASCII Art):** [...]
* **Estrategia IPEE:** Identificar → Plantear → Ejecutar → Evaluar

---

### 2. 📐 Ejercicio Resuelto Paso a Paso
* **Contexto de Electrónica:** [Problema real: polarización BJT, divisor con carga, etc.]
* **Desarrollo Numérico Completo:** [Álgebra paso a paso con unidades]

---

### 3. 📚 Ficha de Repaso Cornell-Kwik
#### 📋 Ficha Técnica (Tabla Markdown)
| Claves / Preguntas Clave | Detalles Técnicos |
| **Concepto / Ley Principal** | [...] |
| **Ecuación Fundamental** | `[Fórmula]` |
| **Error Común a Evitar** | [...] |
| **Relación con Electrónica I y II** | [...] |

#### 💡 Análisis Creativo
* **Analogía (Create):** [...]
* **Duda Crítica (Inquire):** [...]
* **Prueba de Fuego (Apply):** [...]

---

### 4. 🛠️ Herramientas Digitales y Simulación
* **Prompt para Mini App:** [Exhaustive prompt for Gemini Canvas/HTML5]
```

---

## 🔗 Link Convention

**Always use `file://` absolute paths in Markdown links** for project files:
```markdown
[task.md](file:///c:/Users/USER/Documents/wplanchez/Portafolio/Universidad/01_Circuitos/task.md)
```

---

## 🚀 Common Operations

### Viewing the portal locally
```bash
# Open directly in browser (no server needed)
start index.html
# Or navigate to file:///c:/Users/USER/Documents/wplanchez/Portafolio/Universidad/01_Circuitos/index.html
```

### Viewing a simulator
```bash
start apps/01_serie_paralelo/index.html
```

### Checking progress
```bash
cat task.md
```

### Verifying lesson structure
```bash
ls docs/day_01/
```

---

## 📋 Current Project State (as of 2026-10-23)

| Day | Topic | Status | Lessons Done |
|-----|-------|--------|--------------|
| **Day 1** | DC Fundamentals (Ohm, KCL, KVL, Mesh) | ✅ Complete | 4/4 |
| **Day 2** | Voltage/Current Dividers, Biasing Networks | ⏳ Next | 0/3 |
| **Day 3** | Thévenin, Norton, Max Power | ⏳ Pending | 0/3 |
| **Day 4** | Phasors, AC Impedance | ⏳ Pending | 0/3 |
| **Day 5** | RC/RL Transients, τ, Step Response | ⏳ Pending | 0/3 |

**Global progress:** 25% (4 of 16 lessons)

**Next deliverable:** Day 2, Lesson 1 — *Análisis de circuitos serie-paralelo y reducción de redes resistivas*

---

## 🎓 Pedagogical Anchors (Reference Only)

- **NotebookLM:** "Circuitos Eléctricos" — ID `71f7e159-394a-4421-bb9c-608a1d697562` (14 sources: Boylestad, Hayt & Kemmerly, Dorf & Svoboda)
- **Target audience:** Mechatronics engineering students prepping for Electronics I/II
- **Tone:** Senior professor / Principal Hardware Engineer — rigorous, concise, application-oriented

---

## ⚠️ Guardrails

- **Never** generate multiple lessons in one response
- **Never** skip updating `task.md` after a lesson
- **Never** use external JS libraries in simulators (Chart.js, D3, etc. — vanilla only)
- **Never** use relative paths like `./task.md` in responses — use `file://` absolute
- **Always** follow the Cornell-Kwik + IPEE template exactly