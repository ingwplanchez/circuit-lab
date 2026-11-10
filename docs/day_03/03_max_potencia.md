# 📌 Día 3 - Lección 3: Acoplamiento de Impedancias y Transferencia Máxima de Potencia

**Objetivo de Ingeniería / Electrónica:** Determinar la condición exacta de acoplamiento de impedancias ($R_L = R_{TH}$) que maximiza la potencia entregada a una carga, calcular dicha potencia máxima ($P_{max} = V_{TH}^2 / 4R_{TH}$) y entender la implicación del rendimiento del 50% en etapas de salida de audio, adaptadores RF, amplificadores de potencia y sistemas de transmisión de energía.

**Agenda de Tiempo:**
* **Bloque de estudio enfocado (55 min):** Derivación de la condición de máxima potencia, curva $P_L$ vs $R_L$, rendimiento energético, y ejercicio de etapa de salida de amplificador de audio con altavoz de $8\,\Omega$.

---

## 1. 🖊️ Guión Rápido de Repaso

### Fundamentos Teóricos & Conexión Electrónica

Dado un circuito con equivalente Thévenin ($V_{TH}$, $R_{TH}$) que alimenta una carga $R_L$, la potencia entregada a la carga es:

$$P_L = I_L^2 \cdot R_L = \left(\frac{V_{TH}}{R_{TH} + R_L}\right)^2 \cdot R_L$$

Esta función tiene un **máximo** que se obtiene derivando respecto a $R_L$ e igualando a cero:

$$\frac{dP_L}{dR_L} = 0 \quad \Longrightarrow \quad R_L = R_{TH}$$

Cuando $R_L = R_{TH}$, la potencia máxima transferida es:

$$P_{max} = \frac{V_{TH}^2}{4 \cdot R_{TH}}$$

> **Nota crítica de rendimiento:** En el punto de máxima transferencia, la potencia disipada en $R_{TH}$ es **igual** a la entregada a $R_L$ → el rendimiento energético es exactamente η = 50%. En aplicaciones donde la eficiencia importa (fuentes de alimentación, inversores), esto es inaceptable. En aplicaciones donde importa la señal (RF, audio, comunicaciones), se acepta este compromiso.

**Conexión con Electrónica I & II:**

- **Amplificadores de audio:** La impedancia de salida del amplificador ($R_{out} = R_{TH}$) debe ser igual a la impedancia del altavoz ($8\,\Omega$ o $4\,\Omega$) para máxima potencia acústica.
- **Adaptadores RF / Antenas:** Se diseña la red de adaptación para que $Z_L = Z_{TH}^*$ (conjugado complejo en AC), que en CD se reduce a $R_L = R_{TH}$.
- **Etapas de salida BJT/MOSFET:** La resistencia de colector o drenaje óptima se selecciona para maximizar la excursión de señal con la carga conectada.
- **Transmisión de potencia eléctrica:** Se evita deliberadamente el acoplamiento perfecto para mejorar el rendimiento (η > 90%).

---

### Las 3 Fórmulas Esenciales

**1. Condición de Máxima Transferencia de Potencia:**

$$\boxed{R_L^{opt} = R_{TH}} \qquad [\Omega]$$

**2. Potencia Máxima Transferida a la Carga:**

$$\boxed{P_{max} = \frac{V_{TH}^2}{4 \cdot R_{TH}}} \qquad [\text{W}]$$

**3. Potencia General en la Carga (para cualquier $R_L$) y Rendimiento:**

$$P_L = \frac{V_{TH}^2 \cdot R_L}{(R_{TH} + R_L)^2} \qquad \eta = \frac{P_L}{P_{total}} = \frac{R_L}{R_{TH} + R_L} \times 100\,\%$$

---

### Diagrama de Análisis — Procedimiento Visual Máxima Potencia

```text
═══════════════════════════════════════════════════════════════════════════════
 PASO 1 — Obtener equivalente Thévenin de la red fuente (sin R_L)
═══════════════════════════════════════════════════════════════════════════════

    ┌─────────────────────────────┐
    │  RED ACTIVA (V_s, R_1, ...) │
 A──┤                             ├─── A
 B──┤                             ├─── B    ← terminales abiertos
    └─────────────────────────────┘

         ↓   reducción Thévenin

          A
          │
    ┌─────┴──── R_TH ────┐
    │                    │
  [V_TH]              terminal A'
    │
    └──── B (GND)


═══════════════════════════════════════════════════════════════════════════════
 PASO 2 — Conectar R_L variable y expresar P_L en función de R_L
═══════════════════════════════════════════════════════════════════════════════

         A
         │
   ──── R_TH ────┬──── A'
                 │
               [ R_L ]   ← variable (0 → ∞)
                 │
         B ──────┴──── B' (GND)

    I_L = V_TH / (R_TH + R_L)
    P_L = I_L² · R_L  =  V_TH² · R_L / (R_TH + R_L)²


═══════════════════════════════════════════════════════════════════════════════
 PASO 3 — Curva P_L vs R_L: encontrar el máximo por derivada
═══════════════════════════════════════════════════════════════════════════════

    P_L ↑
        │            ★ P_max = V_TH²/(4·R_TH)
        │           /│\
        │          / │ \
        │         /  │  \
        │        /   │   \
        │       /    │    \__________
        │______/_____|_________________ → R_L
               0    R_TH  2·R_TH  3·R_TH

    → Máximo en R_L = R_TH   (dP_L/dR_L = 0)
    → Pendiente positiva si R_L < R_TH  (sub-carga)
    → Pendiente negativa si R_L > R_TH  (sobre-carga)


═══════════════════════════════════════════════════════════════════════════════
 PASO 4 — Análisis de rendimiento energético η
═══════════════════════════════════════════════════════════════════════════════

    η (%) ↑
     100  │                              ___________
          │                         ___/
          │                     ___/
      50  │──────────────── ★ ──────────────────────  ← punto máx. potencia
          │              __/
          │          ___/
          │      ___/
       0  │_____/_________________________________ → R_L
                 0    R_TH

    ★ En R_L = R_TH:   η = 50%   (la misma potencia se pierde en R_TH)
      Si R_L >> R_TH:  η → 100%  (pero P_L → 0)
      Si R_L << R_TH:  η → 0%    (y P_L → 0)

    → Dilema de diseño:  máxima eficiencia  ↔  máxima potencia en carga


═══════════════════════════════════════════════════════════════════════════════
 PASO 5 — Verificación con casos límite
═══════════════════════════════════════════════════════════════════════════════

    Caso A: R_L = 0 (cortocircuito)
    ─────────────────────────────────
         A ──── R_TH ──── A' ═══ B'
         I_sc = V_TH/R_TH  →  P_L = 0  (sin resistencia, no hay disipación)

    Caso B: R_L = R_TH (acoplamiento perfecto) ★
    ─────────────────────────────────────────────
         I_L = V_TH/(2·R_TH)
         P_L = (V_TH/(2·R_TH))² · R_TH = V_TH²/(4·R_TH) = P_max  ✓

    Caso C: R_L → ∞ (circuito abierto)
    ─────────────────────────────────────
         I_L → 0  →  P_L → 0   (V_L = V_TH pero I = 0, sin potencia)
```

---

### Estrategia IPEE de Resolución de Problemas (Paso a Paso)

1. **Identificar:** Obtener (o calcular) el equivalente Thévenin ($V_{TH}$, $R_{TH}$) de la red que alimenta la carga $R_L$. Identificar si el problema pide la $R_L$ óptima, la $P_{max}$, o el rendimiento para una $R_L$ dada.

2. **Plantear:**
   - Si se pide $R_L^{opt}$: aplicar directamente $R_L = R_{TH}$.
   - Si se pide $P_L$ para $R_L$ genérico: usar $P_L = V_{TH}^2 \cdot R_L / (R_{TH}+R_L)^2$.
   - Si se pide rendimiento: $\eta = R_L/(R_{TH}+R_L) \times 100\,\%$.

3. **Ejecutar:** Calcular $P_{max} = V_{TH}^2 / (4 R_{TH})$. Si el problema da $R_L \neq R_{TH}$, calcular la razón $P_L/P_{max}$ para cuantificar el desaprovechamiento.

4. **Evaluar:** Comprobar coherencia: $P_{max}$ debe ocurrir en $R_L = R_{TH}$, $P_{total\_fuente} = V_{TH} \cdot I_L = V_{TH}^2/(2R_{TH})$ y $P_{TH} = P_L = P_{max}$ (η = 50 %).

---

## 2. 📐 Ejercicio Resuelto Paso a Paso (Enfoque Práctico)

**Contexto de Electrónica:** Etapa de salida de un amplificador de audio. El amplificador tiene una impedancia de salida de $R_{out} = 8\,\Omega$ y produce una tensión de circuito abierto $V_{TH} = 12\,\text{V}$ (señal de audio de pico). Se conecta un altavoz de $8\,\Omega$. Se pide:
1. Verificar que el altavoz recibe la máxima potencia.
2. Calcular $P_{max}$ entregada al altavoz.
3. Calcular el rendimiento energético.
4. Comparar con un altavoz de $4\,\Omega$ (sub-carga) y de $16\,\Omega$ (sobre-carga).

---

### ⚡ Paso 1 — Circuito equivalente Thévenin del amplificador

```
        Amplificador (fuente Thévenin)         Altavoz (carga)
        ──────────────────────────────         ───────────────
              R_out = R_TH = 8 Ω
        ┌──────[████████]──────────── A
        │                             │
     [V_TH]                       [R_L = 8 Ω]  ← altavoz
     12 V                             │
        │                             │
        └──────────────────────────── B (GND)
```

> Equivalente Thévenin dado: $V_{TH} = 12\,\text{V}$, $R_{TH} = 8\,\Omega$

---

### ⚡ Paso 2 — Verificar condición de máxima potencia

La condición es $R_L = R_{TH}$:

$$R_L = 8\,\Omega = R_{TH} = 8\,\Omega \quad \checkmark \quad \text{Acoplamiento perfecto}$$

---

### ⚡ Paso 3 — Calcular $P_{max}$ en el altavoz de $8\,\Omega$

```
   R_TH = 8 Ω     R_L = 8 Ω
        ┌──[████]──┬──[████]──┐
        │          │          │
     [V_TH]    V_RTH=6V   V_L=6V
     12 V          │          │
        └──────────┴──────────┘ (GND)

    I_L = 12 V / (8 + 8) Ω = 0.75 A
    V_L = 0.75 A × 8 Ω = 6 V
```

$$I_L = \frac{V_{TH}}{R_{TH}+R_L} = \frac{12\,\text{V}}{8\,\Omega + 8\,\Omega} = \frac{12}{16} = 0.75\,\text{A}$$

$$\boxed{P_{max} = \frac{V_{TH}^2}{4 \cdot R_{TH}} = \frac{(12\,\text{V})^2}{4 \times 8\,\Omega} = \frac{144}{32} = 4.5\,\text{W}}$$

Verificación: $P_{max} = I_L^2 \cdot R_L = (0.75)^2 \times 8 = 0.5625 \times 8 = 4.5\,\text{W}$ ✓

---

### ⚡ Paso 4 — Rendimiento energético en el punto de acoplamiento

Potencia total suministrada por la fuente Thévenin:

$$P_{total} = V_{TH} \cdot I_L = 12\,\text{V} \times 0.75\,\text{A} = 9\,\text{W}$$

Potencia disipada en $R_{TH}$ (calor en el amplificador):

$$P_{RTH} = I_L^2 \cdot R_{TH} = (0.75)^2 \times 8 = 4.5\,\text{W}$$

Rendimiento:

$$\eta = \frac{P_{max}}{P_{total}} = \frac{4.5\,\text{W}}{9\,\text{W}} = 50\,\% \quad \checkmark$$

---

### ⚡ Paso 5 — Comparación con altavoces de distinta impedancia

```
 Escenario        R_L      I_L      V_L      P_L       η
 ─────────────────────────────────────────────────────────────
 Sub-carga        4 Ω    1.000 A   4.0 V   4.00 W    33.3%
 ★ Acoplamiento   8 Ω    0.750 A   6.0 V   4.50 W    50.0%  ← P_max
 Sobre-carga     16 Ω    0.500 A   8.0 V   4.00 W    66.7%
 Sobre-carga     32 Ω    0.308 A   9.8 V   3.02 W    80.0%

 Circuitos (visuales):

 R_L = 4 Ω (sub-carga):
  ──[ R_TH=8Ω ]──[ R_L=4Ω ]──
  I = 12/12 = 1 A   P_L = 1²×4 = 4 W   η = 4/12 = 33%

 R_L = 8 Ω (★ óptimo):
  ──[ R_TH=8Ω ]──[ R_L=8Ω ]──
  I = 12/16 = 0.75A P_L = 4.5 W        η = 50%

 R_L = 16 Ω (sobre-carga):
  ──[ R_TH=8Ω ]──[ R_L=16Ω ]──
  I = 12/24 = 0.5A  P_L = 0.5²×16 = 4W η = 16/24 = 67%
```

> **Conclusión de diseño:** El amplificador entrega la misma potencia ($4\,\text{W}$) tanto con $R_L = 4\,\Omega$ como con $R_L = 16\,\Omega$, pero el rendimiento difiere notablemente. El punto óptimo $R_L = R_{TH} = 8\,\Omega$ maximiza **exclusivamente** la potencia en la carga.

---

## 3. 📚 Ficha de Repaso Cornell-Kwik

### 📋 Ficha Técnica (Estilo Cornell)

| Claves / Preguntas Clave | Detalles Técnicos (Respuestas Directas) |
| :--- | :--- |
| **Condición de máxima potencia** | `R_L = R_TH` (la carga debe igualar la resistencia interna de la fuente) |
| **Fórmula de P_max** | `P_max = V_TH² / (4·R_TH)` — solo depende del equivalente Thévenin |
| **Rendimiento en P_max** | η = 50 % exacto — la otra mitad se pierde en R_TH como calor |
| **¿Qué pasa si R_L > R_TH?** | P_L disminuye pero η aumenta (más eficiente, menos potencia) |
| **¿Qué pasa si R_L < R_TH?** | P_L disminuye y η cae (menos eficiente, menos potencia también) |
| **Error Común a Evitar** | Confundir "máxima potencia" con "máximo rendimiento" — son objetivos opuestos. η = 100% solo cuando R_TH = 0, lo que es imposible físicamente. |
| **Relación con Electrónica I y II** | Amplificadores de audio: R_out del amp = Z del altavoz. Adaptadores RF: conjugado complejo de impedancias. Modelos de salida BJT/MOSFET. |

### 💡 Análisis Creativo (Estilo Kwik)

* **Analogía (Create):** Imagina una manguera (fuente) con una válvula de restricción interna ($R_{TH}$). Si el agujero de salida ($R_L$) es muy pequeño, sale mucha agua pero muy despacio (poca potencia). Si es enorme, sale a mucha presión pero apenas hay caudal (poca potencia también). El diámetro óptimo de salida = diámetro de la restricción interna → **máximo caudal × presión = máxima potencia**.

* **Duda Crítica (Inquire):** *¿Por qué en las plantas eléctricas NO se diseña para máxima transferencia de potencia?* Porque con η = 50 % se desperdiciaría la mitad de la energía generada en las resistencias de los cables y transformadores. La transmisión eléctrica exige η > 95 %, lo que implica trabajar con $R_L \gg R_{TH}$ (tensiones muy altas, corrientes muy bajas).

* **Prueba de Fuego (Apply):** Un transmisor RF tiene $V_{TH} = 50\,\text{V}$ y $R_{TH} = 50\,\Omega$. ¿Cuánto vale $P_{max}$ a la antena si esta tiene $50\,\Omega$?
  *(Respuesta: $P_{max} = 50^2/(4 \times 50) = 2500/200 = 12.5\,\text{W}$. η = 50 %)*

---

## 4. 🛠️ Herramientas Digitales y Simulación

**Simulador interactivo:**  
[`apps/10_max_potencia/index.html`](../../apps/10_max_potencia/index.html)

**Prompt para Mini App Interactiva (Gemini Canvas / HTML5):**

```
Crea un simulador interactivo autónomo en HTML5/CSS3/Vanilla JS titulado
"Transferencia Máxima de Potencia — Acoplamiento de Impedancias".
La app debe incluir:
1. Sliders: V_TH (1-50 V), R_TH (1-200 Ω), R_L (1-500 Ω, variable por el usuario).
2. Indicador visual del punto óptimo: resaltar cuando R_L = R_TH con un badge "★ ACOPLAMIENTO PERFECTO".
3. Gráfica SVG animada de P_L vs R_L: curva en tiempo real, punto actual marcado,
   máximo destacado con línea punteada vertical en R_L = R_TH.
4. Panel de métricas en vivo: I_L, V_L, P_L, P_RTH, P_total, η (%).
5. Tabla comparativa: mostrar P_L para R_L = R_TH/4, R_TH/2, R_TH, 2·R_TH, 4·R_TH.
6. Modo audio: preset altavoz 4/8/16/32 Ω con etiquetas de uso real.
7. Diseño dark dashboard indigo/violet, curva de potencia en gradiente.
```

