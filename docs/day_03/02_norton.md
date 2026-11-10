# 📌 Día 3 - Lección 2: Teorema de Norton y Transformación de Fuentes Reales (V ↔ I)

**Objetivo de Ingeniería / Electrónica:** Dominar el equivalente dual de Thévenin —la fuente Norton ($I_N$ en paralelo con $R_N$)— y la transformación sistemática entre fuentes de tensión real y fuentes de corriente real, herramienta imprescindible para análisis de polarización de transistores BJT con fuentes de señal, análisis de etapas con Op-Amp y cálculo de curvas de transferencia de potencia.

**Agenda de Tiempo:**
* **Bloque de estudio enfocado (60 min):** Equivalente Norton, dualidad Thévenin-Norton, transformación de fuentes y ejercicio de polarización de base BJT con fuente de corriente equivalente.

---

## 1. 🖊️ Guión Rápido de Repaso

### Fundamentos Teóricos & Conexión Electrónica

El **Teorema de Norton** establece que cualquier red lineal de dos terminales puede reemplazarse por una **fuente de corriente ideal $I_N$** en **paralelo** con una resistencia $R_N$.

```
           Red Original                     Equivalente Norton
    ┌──────────────────┐              ┌─────────────────────┐
    │  V, R, fuentes   │              │    ┌─────┐          │
 A──┤                  ├──A        A──┤────┤ R_N ├────┬─────┤──A
    │  (red lineal)    │              │    └─────┘    │     │
 B──┤                  ├──B        B──┤              ↑ I_N  │──B
    └──────────────────┘              │              │      │
                                      └──────────────┴──────┘
```

**Dualidad con Thévenin:**

| Parámetro | Thévenin | Norton |
|:---|:---:|:---:|
| Fuente equivalente | $V_{TH}$ (tensión) | $I_N$ (corriente) |
| Elemento pasivo | $R_{TH}$ **en serie** | $R_N$ **en paralelo** |
| Circuito abierto | $V_{oc} = V_{TH}$ | $V_{oc} = I_N \cdot R_N$ |
| Cortocircuito | $I_{sc} = V_{TH}/R_{TH}$ | $I_{sc} = I_N$ |

**Conexión con Electrónica I & II:**

- En transistores BJT, la red de polarización de base ($R_1 \| R_2$, $V_{CC}$) se transforma a Norton para obtener $I_B$ de forma directa con un solo divisor de corriente.
- En Op-Amps, la transformación de fuentes simplifica el análisis de redes de retroalimentación resistiva.
- Las fuentes de corriente controladas (MOSFET, BJT en saturación) son directamente modelos Norton del transistor.

---

### Las 3 Fórmulas Esenciales

**1. Corriente de cortocircuito Norton** (medir $I_{sc}$ al puentear los terminales A-B):

$$I_N = I_{sc} = \frac{V_{oc}}{R_{TH}}$$

**2. Resistencia Norton** (idéntica a la de Thévenin — apagar fuentes independientes):

$$R_N = R_{TH} = R_{eq}\bigg|_{\text{fuentes independientes apagadas}}$$

**3. Transformación de fuentes** (relación que vincula ambos modelos):

$$V_{TH} = I_N \cdot R_N \qquad \Longleftrightarrow \qquad I_N = \frac{V_{TH}}{R_{TH}}$$

---

### Diagrama de Análisis — Procedimiento Visual Norton

```
PASO 1: Identificar terminales A-B y separar la red de la carga
═══════════════════════════════════════════════════════════════
    ┌─────────────────────────────────┐
    │     RED ACTIVA (sin R_L)        │
    │  (V, R, fuentes independientes) │
 A──┤                                 ├─── A
 B──┤                                 ├─── B  ← aquí va R_L
    └─────────────────────────────────┘

PASO 2: Calcular I_N → cortocircuitar A-B y medir I_sc
═══════════════════════════════════════════════════════
    ┌──────────────────────────────┐
    │     RED ACTIVA               │
 A──┤                              ├──┬── A
    │                              │  │    ← alambre (cortocircuito)
 B──┤                              ├──┘── B
    └──────────────────────────────┘
            I_sc = I_N  →↑  (fluyendo de B a A por el puente)

PASO 3: Calcular R_N → apagar fuentes y ver R_eq desde A-B
═══════════════════════════════════════════════════════════
    ┌──────────────────────────────┐
    │  RED PASIVA                  │
    │  (V→cortocircuito, I→CI)     │
 A──┤                              ├─── A
 B──┤                              ├─── B
    └──────────────────────────────┘
           R_N = R_eq vista desde A-B

PASO 4: Montar el equivalente Norton y reconectar R_L
═════════════════════════════════════════════════════
          A
          │
    ┌─────┴─────┐       ┌─────┐
    │           │       │     │
    ├─── R_N ───┤   A───┤ R_L ├───B
    │           │       │     │
    ↑ I_N       │       └─────┘
    │           │
    └─────┬─────┘
          B (GND)
```

---

### Estrategia IPEE de Resolución de Problemas

1. **Identificar:** Marcar los terminales A-B de interés, localizar las fuentes independientes (de tensión y de corriente) y listar todas las resistencias de la red.

2. **Plantear:**
   - **Para $I_N$:** Puentear A-B con un alambre → aplicar LCK/LVK o superposición para calcular $I_{sc}$.
   - **Para $R_N$:** Apagar fuentes independientes ($V \to$ cortocircuito, $I \to$ circuito abierto) → calcular $R_{eq}$ vista desde A-B.

3. **Ejecutar:** Calcular $I_N$ numéricamente → calcular $R_N$ numéricamente → construir el circuito equivalente → conectar $R_L$ y aplicar divisor de corriente para obtener $I_L$ y $V_L$.

4. **Evaluar:** Verificar con la relación dual: $V_{TH} = I_N \cdot R_N$ y comprobar que $V_L = I_N \cdot (R_N \| R_L)$ coincide con el análisis directo del circuito original.

---

## 2. 📐 Ejercicio Resuelto Paso a Paso (Enfoque Práctico)

**Contexto de Electrónica:** La red de polarización de base de un transistor BJT (NPN, $\beta = 100$) usa $V_{CC} = 12\,\text{V}$, $R_1 = 39\,\text{k}\Omega$ y $R_2 = 10\,\text{k}\Omega$ conectados a la base. Se requiere encontrar el equivalente Norton de la red de polarización vista desde la base (terminales A-B) para calcular directamente la corriente de base $I_B$ como si fuera un simple divisor de corriente.

---

### ⚡ Paso 1 — Circuito Original: Identificar red y terminales A-B

```
        +V_CC = 12 V
             │
            [R1]  39 kΩ
             │
             ├──── A  (Base BJT)
             │
            [R2]  10 kΩ
             │
           ──┴──  GND = B
```

> La red activa entre A y B está formada por: la fuente $V_{CC} = 12\,\text{V}$ en serie con $R_1 = 39\,\text{k}\Omega$ (rama superior) y $R_2 = 10\,\text{k}\Omega$ conectada de A a GND.  
> **Objetivo:** encontrar $I_N$ (con A-B en cortocircuito) y $R_N$ (con $V_{CC}$ apagada).

---

### ⚡ Paso 2 — Calcular $I_N$: Cortocircuitar terminales A-B

Al puentear A-B, $R_2$ queda en cortocircuito (su tensión cae a 0 V, toda la red se simplifica):

```
        +V_CC = 12 V
             │
            [R1]  39 kΩ
             │
        A ───┴──── B  (cortocircuito A-B, R2 en paralelo = 0 Ω)
             │
             ↓ I_sc = I_N    (de A hacia B, sentido convencional)
           ──┴──  GND
```

Con $R_2$ en cortocircuito, la corriente $I_{sc}$ fluye únicamente por $R_1$:

$$I_N = I_{sc} = \frac{V_{CC}}{R_1} = \frac{12\,\text{V}}{39\,\text{k}\Omega} = \mathbf{307.7\,\mu\text{A}}$$

> **Nota:** $R_2$ queda puenteada en este paso → no contribuye a $I_{sc}$.

---

### ⚡ Paso 3 — Calcular $R_N$: Apagar $V_{CC}$ y ver resistencia desde A-B

Al apagar la fuente $V_{CC}$ (reemplazarla por un cortocircuito), la red queda:

```
        ──┬──  (V_CC apagada → cortocircuito al GND)
           │
          [R1]  39 kΩ
           │
      A ───┤
           │
          [R2]  10 kΩ
           │
        ──┴──  GND = B
```

Desde los terminales A-B se ven $R_1$ y $R_2$ **en paralelo** (ambas conectadas entre A y GND):

$$R_N = R_1 \| R_2 = \frac{R_1 \cdot R_2}{R_1 + R_2} = \frac{39\,\text{k}\Omega \times 10\,\text{k}\Omega}{39\,\text{k}\Omega + 10\,\text{k}\Omega} = \frac{390\,\text{k}\Omega^2}{49\,\text{k}\Omega} = \mathbf{7.959\,\text{k}\Omega}$$

---

### ⚡ Paso 4 — Verificación Dual: Comprobar con $V_{TH}$

El equivalente de Thévenin de la misma red es el divisor de tensión:

$$V_{TH} = V_{CC} \cdot \frac{R_2}{R_1 + R_2} = 12\,\text{V} \cdot \frac{10\,\text{k}\Omega}{49\,\text{k}\Omega} = \mathbf{2.449\,\text{V}}$$

Verificamos la identidad de transformación:

$$I_N \cdot R_N = 307.7\,\mu\text{A} \times 7.959\,\text{k}\Omega = \mathbf{2.449\,\text{V}} = V_{TH} \checkmark$$

---

### ⚡ Paso 5 — Equivalente Norton montado: Conectar carga $R_L = r_{\pi}$ del BJT

En el modelo de pequeña señal del BJT, la resistencia de entrada de la base es $r_{\pi} = \beta / g_m$. Con $I_B \approx 10\,\mu\text{A}$ y $\beta = 100$:

$$I_C \approx \beta \cdot I_B = 1\,\text{mA} \qquad g_m = \frac{I_C}{V_T} = \frac{1\,\text{mA}}{26\,\text{mV}} \approx 38.5\,\text{mS}$$
$$r_{\pi} = \frac{\beta}{g_m} = \frac{100}{38.5\,\text{mS}} = 2.6\,\text{k}\Omega$$

```
          A
          │
    ┌─────┴─────┐         ┌────────┐
    │           │         │        │
    ├─── R_N ───┤    A────┤ r_π    ├────GND
    │  7.959kΩ  │         │  2.6kΩ │
    ↑ I_N       │         └────────┘
    │ 307.7µA   │         ← carga real del transistor
    └─────┬─────┘
          B (GND)
```

Corriente de base real (divisor de corriente Norton):

$$I_B = I_N \cdot \frac{R_N}{R_N + r_{\pi}} = 307.7\,\mu\text{A} \cdot \frac{7.959\,\text{k}\Omega}{7.959\,\text{k}\Omega + 2.6\,\text{k}\Omega}$$

$$I_B = 307.7\,\mu\text{A} \cdot \frac{7.959}{10.559} = 307.7\,\mu\text{A} \times 0.7538 = \mathbf{23.2\,\mu\text{A}}$$

Corriente de colector:

$$I_C = \beta \cdot I_B = 100 \times 23.2\,\mu\text{A} = \mathbf{2.32\,\text{mA}}$$

> El equivalente Norton permitió calcular $I_B$ **directamente con un divisor de corriente**, sin plantear ecuaciones de malla completas con la red polarizadora.

---

## 3. 📚 Ficha de Repaso Cornell-Kwik

### 📋 Ficha Técnica (Estilo Cornell)

| Claves / Preguntas Clave | Detalles Técnicos (Respuestas Directas) |
| :--- | :--- |
| **¿Qué es el equivalente Norton?** | Red de dos terminales reducida a una **fuente de corriente $I_N$** en **paralelo** con **$R_N$** |
| **¿Cómo se calcula $I_N$?** | Se cortocircuitan los terminales A-B y se mide $I_{sc}$: `I_N = V_TH / R_TH` |
| **¿Cómo se calcula $R_N$?** | Idéntico a $R_{TH}$: apagar fuentes independientes y ver $R_{eq}$ desde A-B |
| **Relación de transformación** | `V_TH = I_N · R_N` ↔ `I_N = V_TH / R_TH` — siempre se cumple |
| **Error Común a Evitar** | Al cortocircuitar A-B para $I_N$, NO olvidar que las resistencias que estaban en paralelo con A-B quedan puenteadas (corriente = 0 por ellas) |
| **Relación con Electrónica I y II** | La red de polarización BJT ($R_1$, $R_2$, $V_{CC}$) se transforma a Norton → $I_B$ se obtiene con un divisor de corriente simple |

### 💡 Análisis Creativo (Estilo Kwik)

* **Analogía (Create):** Norton es como un surtidor de agua (fuente de corriente $I_N$) con una válvula de resistencia ($R_N$) en paralelo. Si conectas una carga, parte del caudal pasa por ella y parte se "pierde" en la válvula, exactamente como un divisor de corriente.

* **Duda Crítica (Inquire):** *¿Cuándo se prefiere Norton sobre Thévenin?* Cuando la carga está en **paralelo** con la red o cuando la fuente original es de corriente. Thévenin es más natural cuando la carga está en **serie** con la fuente equivalente.

* **Prueba de Fuego (Apply):** Dada una red con $V_s = 10\,\text{V}$, $R_s = 5\,\text{k}\Omega$ y $R_p = 20\,\text{k}\Omega$ en paralelo con A-B: ¿Cuánto vale $I_N$ y $R_N$? 
  *(Respuesta: $I_N = 10\,\text{V}/5\,\text{k}\Omega = 2\,\text{mA}$; $R_N = 5\,\text{k}\Omega \| 20\,\text{k}\Omega = 4\,\text{k}\Omega$)*

---

## 4. 🛠️ Herramientas Digitales y Simulación

**Simulador interactivo:**  
[`apps/09_norton/index.html`](../../apps/09_norton/index.html)

**Prompt para Mini App Interactiva (Gemini Canvas / HTML5):**

```
Crea un simulador interactivo autónomo en HTML5/CSS3/Vanilla JS (sin dependencias externas) 
titulado "Teorema de Norton & Transformación de Fuentes". 
La app debe tener:
1. Panel de controles (sliders): V_s (fuente de tensión, 1-24 V), R1 (1k-100kΩ), 
   R2 (1k-100kΩ), R_L (carga, 1k-50kΩ).
2. Panel de resultados: calcular en tiempo real I_N = V_s/R1, 
   R_N = R1 || R2, V_TH = I_N · R_N, I_L = I_N · R_N/(R_N + R_L), V_L = I_L · R_L.
3. Diagrama SVG animado mostrando el circuito original Y el equivalente Norton 
   side by side, con flechas de corriente animadas proporcionales a los valores.
4. Botón de alternancia: "Ver Norton ↔ Ver Thévenin" que cambia el circuito SVG mostrado.
5. Tabla de verificación: V_TH = I_N·R_N (debe coincidir) con fondo verde si OK, rojo si no.
6. Diseño dark mode dashboard estilo laboratorio electrónico, paleta indigo/violeta.
```

