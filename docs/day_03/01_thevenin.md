# 📌 Día 3 - Lección 1: Teorema de Thévenin y Cálculo de $V_{TH}$ y $R_{TH}$ en Terminales de Interés

**Objetivo de Ingeniería / Electrónica:** Dominar la reducción de cualquier red eléctrica lineal activa de múltiples componentes vista desde dos terminales específicos ($A-B$) a su circuito equivalente de Thévenin ($V_{TH}$ en serie con $R_{TH}$), habilidad imprescindible para modelar la polarización de base en transistores BJT, calcular impedancias de salida en etapas amplificadoras y desacoplar el análisis de circuitos ante cargas variables.

**Agenda de Tiempo:**
* **Bloque de estudio enfocado (40 min):** Principio de equivalencia lineal en bornes, obtención analítica de la tensión de circuito abierto ($V_{oc} = V_{TH}$), métodos de desactivación de fuentes independientes para determinar $R_{TH}$, cálculo de la corriente de cortocircuito ($I_{sc}$), y conexión con la malla de entrada de transistores bipolares.

---

### 1. 🖊️ Guión Rápido de Repaso (Diseñado para dominio conceptual veloz)

* **Fundamentos Teóricos & Conexión Electrónica:**
  * El **Teorema de Thévenin** establece que cualquier red dipolo lineal compuesta por resistencias, fuentes independientes y dependientes puede reemplazarse por completo, respecto a dos terminales $A$ y $B$, por un circuito equivalente formado únicamente por una **fuente de tensión independiente $V_{TH}$** conectada en serie con una **resistencia equivalente $R_{TH}$**.
  * **Conexión con Electrónica I y II:**
    1. **Polarización Universal por Divisor de Base en BJT:** Es la aplicación estandarte en electrónica discreta. El divisor formado por $R_1$, $R_2$ y la fuente $V_{CC}$ se sustituye directamente por su equivalente Thévenin:
       $$V_{TH} = V_{CC} \cdot \left( \frac{R_2}{R_1 + R_2} \right), \quad R_{TH} = R_1 \parallel R_2 = \frac{R_1 \cdot R_2}{R_1 + R_2}$$
       Esto reduce la red de entrada del transistor a una única malla simple: $V_{TH} - I_B R_{TH} - V_{BE} - I_E R_E = 0$, permitiendo despejar la corriente de base $I_B$ de manera inmediata.
    2. **Impedancia de Salida ($Z_{out}$ o $R_{out}$):** La resistencia de Thévenin representa la impedancia interna con la que una etapa preamplificadora entrega señal a la etapa siguiente, determinando el nivel de atenuación bajo carga.
    3. **Análisis con Carga Variable:** En lugar de recalcular todo el circuito cada vez que cambia el receptor o actuador ($R_L$), solo se sustituye el valor de $R_L$ en el modelo Thévenin simplificado de una sola malla.

* **Las 3 Fórmulas Esenciales:**
  1. **Tensión de Thévenin ($V_{TH}$ o Tensión a Circuito Abierto):**
     $$V_{TH} = V_{oc} = V_A - V_B \quad \text{(retirando la carga } R_L \text{)} \quad [\text{V}]$$

  2. **Resistencia de Thévenin ($R_{TH}$ con Fuentes Independientes Apagadas):**
     $$R_{TH} = R_{AB} \quad \text{(Fuentes de tensión } \to 0\text{ V [Cortocircuito]}, \text{ Fuentes de corriente } \to 0\text{ A [Circuito abierto]}) \quad [\Omega]$$

  3. **Tensión y Corriente en la Carga $R_L$ con el Circuito Equivalente:**
     $$I_L = \frac{V_{TH}}{R_{TH} + R_L} \quad \implies \quad V_L = I_L \cdot R_L = V_{TH} \cdot \left( \frac{R_L}{R_{TH} + R_L} \right) \quad [\text{A, V}]$$

* **Diagrama de Análisis (Red Compleja vs Equivalente Thévenin):**

```text
       Circuito Lineal Original                       Circuito Equivalente Thévenin
       
   ┌───────────────────────────┐   Terminal A                Terminal A
   │                           o───────┐               ┌───────[ R_TH ]───────o───────┐
   │ Red Lineal con Fuentes    │       │               │                      │       │
   │ Independientes y Pasivos  │      [RL]           [V_TH]                  [RL]   (V_L)
   │                           │       │               │                      │       │
   │                           o───────┘               └──────────────────────o───────┘
   └───────────────────────────┘   Terminal B                Terminal B
```

---

### Diagrama de Análisis — Procedimiento Visual Thévenin

```text
═══════════════════════════════════════════════════════════════════════════════
 PASO 1 — Identificar terminales A-B y desconectar la carga R_L
═══════════════════════════════════════════════════════════════════════════════

    ┌─────────────────────────────────────────────┐
    │                                             │
    │     RED ACTIVA ORIGINAL                     │
    │  (V_s, fuentes, R_1, R_2, R_3 ...)          │
    │                                             │
 A──┤                                             ├─── A ←──┐
    │                                             │         │  R_L
 B──┤                                             ├─── B ←──┘  (desconectada)
    └─────────────────────────────────────────────┘

    → El par de bornes A-B queda a CIRCUITO ABIERTO.
    → Objetivo: encontrar V_AB = V_TH y R_AB = R_TH.


═══════════════════════════════════════════════════════════════════════════════
 PASO 2 — Calcular V_TH: medir tensión a circuito abierto (V_oc = V_AB)
═══════════════════════════════════════════════════════════════════════════════

    ┌─────────────────────────────────────────────┐
    │     RED ACTIVA (con fuentes encendidas)     │
    │                                             │
 A──┤                                             ├─── A
    │                                             │     │
 B──┤                                             ├─── B     ← Sin carga
    └─────────────────────────────────────────────┘     │
                                                        │
                                               V_TH = V_oc
                                               (se mide entre A y B
                                                con voltímetro ideal,
                                                sin corriente circulando)

    → Usar divisor de tensión, análisis de nodos o LVK.
    → V_TH = V_oc = V_A − V_B


═══════════════════════════════════════════════════════════════════════════════
 PASO 3 — Calcular R_TH: apagar fuentes y medir R_eq desde A-B
═══════════════════════════════════════════════════════════════════════════════

    Regla de apagado de fuentes:
    ┌─────────────────────────────────────────────────┐
    │  Fuente de tensión V_s  →  reemplazar por ═══  │  (cortocircuito, alambre)
    │  Fuente de corriente I_s →  reemplazar por ···  │  (circuito abierto)
    └─────────────────────────────────────────────────┘

    ┌─────────────────────────────────────────────┐
    │     RED PASIVA (fuentes independientes      │
    │     apagadas, sólo resistencias)            │
 A──┤                                             ├─── A
    │                                             │     │
 B──┤                                             ├─── B   ←── R_ohmetro virtual
    └─────────────────────────────────────────────┘

    → R_TH = R_eq vista desde A-B = combinación serie/paralelo de resistencias.


═══════════════════════════════════════════════════════════════════════════════
 PASO 4 — Montar el equivalente Thévenin y reconectar R_L
═══════════════════════════════════════════════════════════════════════════════

          A
          │
    ┌─────┴──────[ R_TH ]──────┐
    │                          │
  [V_TH]                    ┌──┴──┐
    │  +                    │ R_L │  ← carga reconectada
    │  −                    └──┬──┘
    └─────────────────────────┘
          B (GND)

    → I_L = V_TH / (R_TH + R_L)     ← Ley de Ohm directa en una malla
    → V_L = I_L × R_L               ← divisor de tensión Thévenin


═══════════════════════════════════════════════════════════════════════════════
 PASO 5 — Evaluación de límites (verificación física)
═══════════════════════════════════════════════════════════════════════════════

    Caso A: R_L → ∞  (circuito abierto)
    ┌──────────────────────────────────────────┐
    │  R_TH ──── A                             │
    │                                          │
    │ [V_TH]        ···  (sin carga)  V_L→V_TH│
    │                                          │
    │  GND  ──── B                             │
    └──────────────────────────────────────────┘
    → Toda la tensión cae en A-B: V_L = V_TH ✓

    Caso B: R_L → 0  (cortocircuito)
    ┌──────────────────────────────────────────┐
    │  R_TH ──── A ═══ B  (puente cortocircuito│
    │                                          │
    │ [V_TH]       I_sc = V_TH / R_TH          │
    │                                          │
    │  GND  ──── B                             │
    └──────────────────────────────────────────┘
    → Corriente máxima: I_sc = V_TH / R_TH ✓
    → Debe coincidir con I_sc medido directamente en la red original.
```

---

* **Estrategia IPEE de Resolución de Problemas (Paso a Paso):**
  1. *Identificar:* Desconectar físicamente la resistencia de carga $R_L$ del circuito. Identificar y etiquetar claramente los dos terminales resultantes ($A$ y $B$).
  2. *Plantear:*
     * **Para $V_{TH}$:** Analizar el circuito a circuito abierto entre $A$ y $B$ para hallar $V_{AB} = V_A - V_B$ utilizando divisor de tensión, análisis de nodos o mallas.
     * **Para $R_{TH}$:** Apagar todas las fuentes independientes (sustituir fuentes de tensión independientes por cables/cortocircuitos y fuentes de corriente por circuitos abiertos) y calcular la resistencia equivalente vista desde los terminales $A-B$.
  3. *Ejecutar:* Dibujar el circuito serie equivalente con $V_{TH}$ y $R_{TH}$. Reconectar la carga $R_L$ entre los terminales $A$ y $B$ y resolver la corriente $I_L$ mediante la Ley de Ohm directa: $I_L = V_{TH} / (R_{TH} + R_L)$.
  4. *Evaluar:* Verificar los límites físicos:
     * Si $R_L \to \infty$ (circuito abierto), $V_L = V_{TH}$.
     * Si $R_L \to 0$ (cortocircuito), la corriente debe coincidir exactamente con la corriente de cortocircuito directa de la red original: $I_{sc} = V_{TH} / R_{TH}$.

---

### 2. 📐 Ejercicio Resuelto Paso a Paso (Enfoque Práctico)

* **Contexto de Electrónica:** Modelado y simplificación de una red de alimentación y polarización que alimenta una carga resistiva externa variable $R_L$. El circuito original cuenta con una fuente de alimentación continua $V_s = 20\text{ V}$, una resistencia serie de paso $R_1 = 1\text{ k}\Omega$, una resistencia en derivación $R_2 = 2.2\text{ k}\Omega$ y una resistencia de acoplamiento de salida $R_3 = 470\,\Omega$. La carga conectada es $R_L = 1\text{ k}\Omega$.

* **Diagrama Esquemático del Circuito Original:**

```text
               I_1                      R3 = 470 Ω         Terminal A
        ┌─────>───[ R1 = 1 kΩ ]────┬───────[====]──────────────●────────┐
        │                          │                           │        │
      + │                          │                           │       [RL]
  ( Vs = 20 V )              [ R2 = 2.2 kΩ ]                 (Voc)    1 kΩ
      - │                          │                           │        │
        │                          │                           │        │
        └──────────────────────────┴───────────────────────────●────────┘
                                                           Terminal B (GND)
```

* **Desarrollo Numérico Completo:**

  1. **Paso 1: Cálculo de la Tensión de Thévenin ($V_{TH} = V_{oc}$):**
     * Retiramos la carga $R_L$ entre los terminales $A$ y $B$.
     * Como los terminales $A$ y $B$ quedan a circuito abierto, por la resistencia $R_3$ no puede circular corriente ($I_{R3} = 0\text{ A}$).
     * Por lo tanto, no hay caída de tensión en $R_3$ ($V_{R3} = 0\text{ V}$), lo que significa que el potencial del terminal $A$ es exactamente igual al potencial del nodo intermedio entre $R_1$ y $R_2$.

     * **Diagrama del Circuito a Circuito Abierto ($V_{oc}$):**
```text
               I_1                      R3 = 470 Ω         Terminal A (VA)
        ┌─────>───[ R1 = 1 kΩ ]────┬───────[====]──────────────○
        │                          │        (I_R3 = 0 A)       │
      + │                          │                           │ +
  ( Vs = 20 V )              [ R2 = 2.2 kΩ ]                 V_TH = V_oc = 13.75 V
      - │                          │ (V_nodo = 13.75 V)        │ -
        │                          │                           │
        └──────────────────────────┴───────────────────────────○
                                                           Terminal B (VB = GND)
```

  * Aplicamos la fórmula del divisor de tensión sobre $R_2$:
  $$V_{TH} = V_{oc} = V_s \cdot \left( \frac{R_2}{R_1 + R_2} \right) = 20\text{ V} \cdot \left( \frac{2200\,\Omega}{1000\,\Omega + 2200\,\Omega} \right) = 20\text{ V} \cdot \frac{2200}{3200} = 13.75\text{ V}$$

  2. **Paso 2: Cálculo de la Resistencia de Thévenin ($R_{TH}$):**
     * Desactivamos la fuente independiente de tensión $V_s \to 0\text{ V}$ (reemplazándola por un cortocircuito / cable directo a tierra).
     * Miramos la resistencia equivalente "hacia adentro" desde los terminales $A$ y $B$:

     * **Diagrama con Fuente Desactivada ($R_{TH} = R_{AB}$):**
```text
           (Vs Apagado = Corto)         R3 = 470 Ω         Terminal A
        ┌──────────( Cable )───────┬───────[====]──────────────○ ◄──┐
        │                          │                                │  R_TH vista
        │                          │                                │  desde A-B
        │                    [ R2 = 2.2 kΩ ]                        │
        │ [ R1 = 1 kΩ ]            │                                │  R_TH = 1157.5 Ω
        │                          │                                │
        └──────────────────────────┴───────────────────────────○ ◄──┘
                                                           Terminal B
       │◄────── R1 || R2 = 687.5 Ω ─────►│
```

  * Las resistencias $R_1$ y $R_2$ quedan en paralelo entre el nodo intermedio y tierra:
    $$R_{1 \parallel 2} = \frac{R_1 \cdot R_2}{R_1 + R_2} = \frac{1000 \cdot 2200}{1000 + 2200} = \frac{2,200,000}{3200} = 687.5\,\Omega$$
  * La resistencia $R_3$ se encuentra en serie con dicho arreglo en paralelo:
    $$R_{TH} = R_3 + R_{1 \parallel 2} = 470\,\Omega + 687.5\,\Omega = 1157.5\,\Omega \approx 1.158\text{ k}\Omega$$

  3. **Paso 3: Construcción del Circuito Equivalente Thévenin:**
     El circuito completo se reduce al siguiente esquema elemental de una sola malla:

```text
               R_TH = 1157.5 Ω         Terminal A
         ┌─────────[====]──────────────────●────────┐
         │                                 │        │
       + │                                 │       [RL]
  ( V_TH = 13.75 V )                      (VL)     1 kΩ
       - │                                 │        │
         │                                 │        │
         └─────────────────────────────────●────────┘
                                       Terminal B
```

  4. **Paso 4: Cálculo de Corriente y Voltaje en la Carga $R_L = 1\text{ k}\Omega$:**
     * Conectamos la carga $R_L$ al equivalente Thévenin y calculamos la corriente de malla $I_L$:

     * **Diagrama de Malla Única con Carga $R_L$:**
```text
                     I_L = 6.373 mA --->
               R_TH = 1157.5 Ω         Terminal A
         ┌─────────[====]──────────────────●────────┐
         │       (V_RTH = 7.377 V)         │        │
       + │                                 │        ▼ I_L
  ( V_TH = 13.75 V )                       │       [RL = 1 kΩ]
       - │                                (VL)    (V_L = 6.373 V)
         │                                 │        │
         └─────────────────────────────────●────────┘
                                       Terminal B
```

  * **Corriente en la carga ($I_L$):**
    $$I_L = \frac{V_{TH}}{R_{TH} + R_L} = \frac{13.75\text{ V}}{1157.5\,\Omega + 1000\,\Omega} = \frac{13.75\text{ V}}{2157.5\,\Omega} \approx 6.373\text{ mA}$$

  * **Tensión en la carga ($V_L$):**
    $$V_L = I_L \cdot R_L = 6.373\text{ mA} \times 1000\,\Omega \approx 6.373\text{ V}$$

  5. **Paso 5: Verificación Cruzada (Sin Thévenin, por Reducción Directa del Circuito Original):**
     * Para confirmar la validez del método, resolvemos el circuito original completo con $R_L = 1\text{ k}\Omega$ conectado:

     * **Diagrama del Circuito Original Completo con Telemetría de Verificación:**
```text
               I_total = 10.63 mA       I_R3 = 6.37 mA     Terminal A
        ┌─────>───[ R1 = 1 kΩ ]────┬───────[ 470 Ω ]───────────●────────┐
        │        (VR1 = 10.63 V)   │                           │        │
      + │                          │                           │       [RL]
  ( Vs = 20 V )              [ R2 = 2.2 kΩ ]                  (VL)     1 kΩ
      - │                    (VR2 = 9.37 V)                 6.373 V     │
        │                    (IR2 = 4.26 mA)                   │        │
        └──────────────────────────┴───────────────────────────●────────┘
                                                           Terminal B (GND)
```

  * En el circuito original con $R_L = 1\text{ k}\Omega$, la rama derecha tiene: $R_{3} + R_L = 470 + 1000 = 1470\,\Omega$.
  * En paralelo con $R_2 = 2200\,\Omega$:
    $$R_{eq\_paralelo} = \frac{2200 \times 1470}{2200 + 1470} = \frac{3,234,000}{3670} \approx 881.20\,\Omega$$
  * Resistencia total vista por la fuente: $R_{total} = R_1 + R_{eq\_paralelo} = 1000 + 881.20 = 1881.20\,\Omega$.
  * Tensión en el nodo central:
    $$V_{nodo} = 20\text{ V} \cdot \left( \frac{881.20}{1881.20} \right) \approx 9.3685\text{ V}$$
  * Tensión en la carga $R_L$ por divisor entre $R_3$ y $R_L$:
    $$V_L = V_{nodo} \cdot \left( \frac{R_L}{R_3 + R_L} \right) = 9.3685\text{ V} \cdot \left( \frac{1000}{1470} \right) \approx 6.373\text{ V} \quad \checkmark$$
  * *¡Coincidencia matemática exacta al $100\%$! Con Thévenin se resolvió con una simple división de una sola línea.*

---

### 3. 📚 Ficha de Repaso Cornell-Kwik (Para Dominio Rápido)

#### 📋 Ficha Técnica (Estilo Cornell)
| Claves / Preguntas Clave | Detalles Técnicos (Respuestas Directas) |
| :--- | :--- |
| **Concepto Fundamental** | Cualquier circuito lineal dipolo se reduce a una fuente real de tensión ($V_{TH}$ en serie con $R_{TH}$) respecto a 2 terminales. |
| **Cálculo de $V_{TH}$** | Tensión a circuito abierto entre terminales: $V_{TH} = V_{oc} = V_A - V_B$ (con $R_L$ desconectada). |
| **Cálculo de $R_{TH}$** | Resistencia de entrada vista desde los terminales con fuentes independientes apagadas ($V \to$ corto, $I \to$ abierto). |
| **Error Típico a Evitar** | Olvidar retirar la resistencia de carga $R_L$ antes de calcular $V_{TH}$ o $R_{TH}$, o apagar fuentes dependientes como si fueran independientes. |
| **Relación con Electrónica I y II** | Simplificación de la polarización de base en BJT ($V_{TH} = V_{BB}, R_{TH} = R_B$), cálculo de la impedancia de salida $R_{out}$ en amplificadores operacionales y etapas de emisor/colector común. |

#### 💡 Análisis Creativo (Estilo Kwik)
* **Analogía (Create):** El circuito de Thévenin es como una batería de automóvil real. Una batería comercial nunca es una fuente pura de $12\text{ V}$; tiene una tensión en bornes sin carga ($V_{TH} = 12.6\text{ V}$) y una resistencia química interna ($R_{TH} = 0.02\,\Omega$). Cuando conectas el motor de arranque ($R_L$), la tensión cae debido a $R_{TH}$. El Teorema de Thévenin demuestra que **cualquier circuito lineal del mundo se comporta exactamente igual que una batería real con resistencia interna**.
* **Duda Crítica (Inquire):** *¿Qué ocurre si el circuito contiene fuentes dependientes (controladas por corriente o tensión)?*
  No se pueden apagar las fuentes dependientes porque dependen de variables del circuito. En ese caso, $R_{TH}$ se calcula aplicando una **fuente de prueba auxiliar** ($V_{\text{prueba}} = 1\text{ V}$ o $I_{\text{prueba}} = 1\text{ A}$) en los terminales $A-B$ y calculando $R_{TH} = V_{\text{prueba}} / I_{\text{prueba}}$, o calculando la corriente de cortocircuito $I_{sc}$ y aplicando $R_{TH} = V_{oc} / I_{sc}$.
* **Prueba de Fuego (Apply):** Si un circuito entrega $V_{oc} = 10\text{ V}$ sin carga y su corriente de cortocircuito directa es $I_{sc} = 2\text{ mA}$, ¿cuánto vale su resistencia de Thévenin?
  *Respuesta:* $R_{TH} = \frac{V_{oc}}{I_{sc}} = \frac{10\text{ V}}{2\text{ mA}} = \mathbf{5\text{ k}\Omega}$. ¡En 5 segundos sin ver el diagrama interno!

---

### 4. 🛠️ Herramientas Digitales y Simulación

* **Prompt para Mini App Interactiva (Gemini Canvas / HTML5):**
> *"Genera una aplicación web interactiva en un solo archivo HTML5/CSS/JS autocontenido con Tailwind CSS y estética de laboratorio electrónico en modo oscuro. Debe simular y comparar lado a lado un Circuito Resistivo Original con Fuente $V_s$ ($5\text{ V}$ a $30\text{ V}$), $R_1$, $R_2$ y $R_3$ frente a su Circuito Equivalente de Thévenin ($V_{TH}$ y $R_{TH}$). La aplicación debe permitir modificar los componentes con sliders, desconectar la carga $R_L$ para verificar que la tensión en bornes coincide exactamente con $V_{TH}$, y variar $R_L$ ($100\,\Omega$ a $10\text{ k}\Omega$) para demostrar en tiempo real que tanto el circuito original como el modelo Thévenin entregan exactamente la misma corriente $I_L$, el mismo voltaje $V_L$ y la misma potencia a la carga."*

