# 📌 Día 2 - Lección 1: Análisis de Circuitos Serie-Paralelo y Reducción de Redes Resistivas

**Objetivo de Ingeniería / Electrónica:** Dominar la descomposición modular y reducción sistemática de redes resistivas combinadas (redes en escalera multietapa, topologías en T y $\pi$, y puentes resistivos) para determinar la resistencia de entrada equivalente ($R_{in}$ o $R_{eq}$) y las tensiones nodales intermedias que fijan el punto estático de polarización ($Q$) e impedancias de entrada en etapas analógicas con transistores BJT y MOSFET.

**Agenda de Tiempo:**
* **Bloque de estudio enfocado (35 min):** Clasificación topológica rigurosa de nodos y ramas, algoritmo de reducción progresiva "de derecha a izquierda" (carga hacia la fuente), cálculo de impedancia vista desde terminales y análisis de puentes resistivos.

---

### 1. 🖊️ Guión Rápido de Repaso (Diseñado para dominio conceptual veloz)

* **Fundamentos Teóricos & Conexión Electrónica:**
  * En circuitos discretos e integrados reales, las resistencias rara vez se encuentran en configuraciones estrictamente serie o puramente paralelo. Se agrupan en **redes combinadas serie-paralelo**. Para que dos componentes estén en serie, deben compartir un único nodo exclusivo por el que circule exactamente la misma corriente. Para que estén en paralelo, deben compartir ambos pares de nodos, experimentando la misma diferencia de potencial.
  * **Conexión con Electrónica I y II:** 
    1. **Impedancia de Entrada ($R_{in}$):** Al acoplar una etapa amplificadora (como un par diferencial o un emisor común con degeneración de emisor) con una red de realimentación, el circuito equivalente de entrada es una red serie-paralelo que carga al generador de señal o sensor.
    2. **Atenuadores y Redes Escalera (R-2R):** Los convertidores digital-analógico (DAC) y las redes de atenuación pasiva balanceadas basan su precisión en cómo la corriente se bifurca en cada celda serie-paralelo sucesiva.
    3. **Polarización con Múltiples Puntos de Operación:** Redes resistivas en cascada permiten derivar voltajes de polarización fijos para varias etapas de amplificación simultáneas a partir de un único carril de alimentación $V_{CC}$.

* **Las 3 Fórmulas Esenciales:**
  1. **Reducción Paralelo por Conductancias y Dos Ramas:**
     $$R_p = \frac{R_a \cdot R_b}{R_a + R_b} \quad \iff \quad G_{eq} = \sum_{k=1}^N \frac{1}{R_k} \quad [\Omega \text{ o S}]$$

  2. **Ecuación Recurrente de Red en Escalera (Impedancia Vista hacia la Carga):**
     $$R_{in, k} = R_{serie, k} + \left( R_{shunt, k} \parallel R_{in, k+1} \right) \quad [\Omega]$$

  3. **Condición de Equilibrio en Puente Resistivo (Wheatstone):**
     $$\frac{R_1}{R_2} = \frac{R_3}{R_4} \iff V_A - V_B = 0\text{ V} \quad [\text{V}]$$

* **Diagrama de Análisis (Red Combinada Serie-Paralelo Multietapa):**

```text
       (Nodo 1)             (Nodo 2)             (Nodo 3)
   +------o--------[ R1 ]------o--------[ R3 ]------o-----+
   |      |                    |                    |     |
  [Vs]    |                   [R2]                 [R4]  [RL] (Carga)
   |      | (V1 = Vs)          |                    |     |
   +------o--------------------o--------------------o-----+
      (Masa / Tierra = 0 V)
```
*Estrategia de reducción visual:* Se resuelve de derecha a izquierda: $R_p = R_4 \parallel R_L \rightarrow R_{serie} = R_3 + R_p \rightarrow R_{eq2} = R_2 \parallel R_{serie} \rightarrow R_{total} = R_1 + R_{eq2}$.

* **Estrategia IPEE de Resolución de Problemas (Paso a Paso):**
  1. *Identificar:* Etiquetar todos los nodos esenciales. Identificar la pareja de resistencias más alejada de la fuente de excitación que comparta una condición pura de serie o paralelo.
  2. *Plantear:* Establecer un plan de simplificación modular iterativo ("de adentro hacia afuera"), calculando equivalentes locales ($R_{eq1}, R_{eq2}, \dots$) sin perder el mapeo de los nodos originales de interés.
  3. *Ejecutar:* Reducir la red a una sola resistencia equivalente total $R_{in}$ vista por la fuente. Hallar la corriente total suministrada ($I_{total} = V_s / R_{in}$) y desandar el camino mediante divisores sucesivos de voltaje y corriente para determinar las tensiones nodales y corrientes de rama.
  4. *Evaluar:* Comprobar que en cada nodo se cumpla LCK ($\sum I = 0$), en cada malla LVK ($\sum V = 0$) y que el balance de potencias sea rigurosamente conservativo: $P_{\text{fuente}} = \sum P_{\text{disipada}}$.

* **Taxonomía y Funciones de Resistencias en Redes Electrónicas:**
  En circuitos discretos e integrados, una resistencia no solo "limita corriente", sino que cumple funciones topológicas muy diferenciadas según su ubicación en la red:

  #### 1. Resistencia de Acoplamiento (o de Enlace Interetapa)
  * **Qué es:** Componente resistivo (frecuentemente asociado a redes $RC$ o divisores en cascada) ubicado en serie en la trayectoria de señal entre dos etapas sucesivas (por ejemplo, entre la salida de un preamplificador y la entrada de una etapa de potencia).
  * **Para qué sirve:** Conduce y transfiere la señal útil de una etapa a la siguiente, ajusta la impedancia mutua de transferencia, atenúa niveles excesivos para evitar saturación y aísla la carga de la salida del bloque anterior.
  ```text
       Etapa 1 (Generador)              Enlace                  Etapa 2 (Receptor)
     +---------------------+          [ R_acop ]             +---------------------+
     |                     |           (R_enlace)            |                     |
     | Salida Preamp o V_A o────────────[====]───────────────o Entrada Etapa 2     |
     |                     |                                 | (o Nodo B)          |
     +---------------------+                                 +---------------------+
  ```

  #### 2. Resistencia Shunt (o de Derivación / Censado)
  * **Qué es:** Resistor conectado en paralelo con un instrumento de medida, o colocado directamente en una rama a masa (tierra) / línea de corriente. En instrumentación suele ser de valor óhmico muy bajo ($m\Omega$ a pocos $\Omega$) y alta precisión; en redes de polarización representa una rama en derivación hacia el carril de referencia.
  * **Para qué sirve:** Desvía parte de la corriente de una línea principal y actúa como transductor corriente-voltaje ($V_{sense} = I \cdot R_{shunt}$) para que un microcontrolador, amplificador de instrumentación o circuito de protección lea la corriente sin perturbar el sistema.
  ```text
            Línea Principal de Corriente (I_total)
     ───────o───────────────────────────────────────o───────► Hacia la Carga
            │                                       │
           [+]                                     [-]
            │   ┌───────────────────────────────┐   │  (Medición diferencial)
            └───┤   R_shunt (Bajo valor, mΩ)    ├───┘  ΔV = I_total · R_shunt
                └───────────────────────────────┘
  ```

  #### 3. Resistencia de Carga Local
  * **Qué es:** Componente resistivo pasivo que pertenece de manera interna e intrínseca al subsistema, módulo o celda activa local (por ejemplo, la resistencia de colector $R_C$ o drenador $R_D$ dentro de una etapa amplificadora, o un resistor fijador de nodo a tierra como $R_4$ en una celda de polarización).
  * **Para qué sirve:** Consume energía localmente para transformar las variaciones de corriente de un dispositivo activo en variaciones de tensión, define el punto estático de reposo ($Q$) y fija la impedancia interna de salida de esa etapa específica antes de conectarle cargas externas.
  ```text
                 +V_CC (Alimentación Local)
                   │
                 [ R_local ] (ej. R_C o fijadora local de celda)
                   │
     V_in ──────► [ Transistor / Etapa Local ]
                   │
                   o────────────────────────────► V_out (Salida de la celda local)
                   │
                  GND
  ```

  #### 4. Resistencia de Carga Externa ($R_L$)
  * **Qué es:** Es la impedancia o resistencia del dispositivo receptor final, actuador o subsistema exterior que se conecta desde el exterior a los terminales de salida de una fuente o etapa (ejemplo: un altavoz de $8\,\Omega$, una bobina de relé, un sensor o la impedancia de entrada $R_{in}$ del siguiente equipo).
  * **Para qué sirve:** Representa el trabajo útil o destino final donde se entrega la potencia procesada. Su presencia modifica la impedancia equivalente total y provoca el fenómeno conocido como **efecto de carga** (caída de tensión por drenaje de corriente adicional).
  ```text
       Circuito / Etapa de Salida                    Dispositivo Externo Conectado
     +───────────────────────────+                     (Altavoz, Motor, Carga RL)
     │                           │                         ┌───────────────┐
     │ Terminal de Salida (+)    o─────────────────────────┤               │
     │                           │                         │  R_L (Carga   │
     │                           │                         │   Externa)    │
     │ Terminal de Retorno (-)   o─────────────────────────┤               │
     │                           │                         └───────────────┘
     +───────────────────────────+
  ```

---

### 2. 📐 Ejercicio Resuelto Paso a Paso (Enfoque Práctico)

* **Contexto de Electrónica:** Red de polarización y distribución de tensión para una etapa preamplificadora de instrumentación. La fuente de alimentación continua es $V_{CC} = 24\text{ V}$. Se dispone de una resistencia de paso inicial $R_1 = 470\,\Omega$, un ramal en derivación $R_2 = 1.5\text{ k}\Omega$, una resistencia intermedia $R_3 = 680\,\Omega$, un elemento de fijación $R_4 = 1.2\text{ k}\Omega$ y la resistencia de entrada de la etapa siguiente (carga) $R_L = 3.3\text{ k}\Omega$.

* **Diagrama del Circuito:**
```text
           I_total           I_R3
      +----->--[ R1 ]---+---->---[ R3 ]----+--------+
      |        470 Ω    |        680 Ω     |        |
      |                 |                  |        |
    [Vcc]              [R2]               [R4]     [RL]
    24 V              1.5 kΩ             1.2 kΩ   3.3 kΩ
      |                 |                  |        |
      |     (Nodo A)    |      (Nodo B)    |        |
     GND -------------- o ---------------- o -------+
```

* **Desarrollo Numérico Completo:**

  1. **Paso 1: Simplificación del bloque final de carga (Nodo B):**
     Las resistencias $R_4$ y $R_L$ se encuentran en paralelo directo entre el Nodo B y tierra:
     $$R_{4 \parallel L} = \frac{R_4 \cdot R_L}{R_4 + R_L} = \frac{1200 \cdot 3300}{1200 + 3300} = \frac{3,960,000}{4500} = 880\,\Omega$$

  2. **Paso 2: Suma en serie con la rama de enlace $R_3$:**
     La rama que sale del Nodo A hacia la derecha contiene $R_3$ en serie con el bloque equivalente $R_{4 \parallel L}$:
     $$R_{\text{rama\_derecha}} = R_3 + R_{4 \parallel L} = 680\,\Omega + 880\,\Omega = 1560\,\Omega = 1.56\text{ k}\Omega$$

  3. **Paso 3: Paralelo en el Nodo A:**
     En el Nodo A, la resistencia en derivación $R_2$ queda en paralelo con la rama derecha completa:
     $$R_{A} = \frac{R_2 \cdot R_{\text{rama\_derecha}}}{R_2 + R_{\text{rama\_derecha}}} = \frac{1500 \cdot 1560}{1500 + 1560} = \frac{2,340,000}{3060} \approx 764.71\,\Omega$$

  4. **Paso 4: Resistencia equivalente total vista por la fuente ($R_{in}$):**
     La resistencia $R_1$ está en serie con todo el bloque equivalente del Nodo A:
     $$R_{total} = R_1 + R_A = 470\,\Omega + 764.71\,\Omega = 1234.71\,\Omega \approx 1.235\text{ k}\Omega$$

  5. **Paso 5: Corriente total y tensiones nodales:**
     * **Corriente total de la fuente:**
       $$I_{total} = \frac{V_{CC}}{R_{total}} = \frac{24\text{ V}}{1234.71\,\Omega} \approx 19.438\text{ mA}$$

     * **Tensión en el Nodo A ($V_A$):**
       $$V_A = V_{CC} - (I_{total} \cdot R_1) = 24\text{ V} - (19.438\text{ mA} \cdot 470\,\Omega) = 24\text{ V} - 9.136\text{ V} = 14.864\text{ V}$$
       *(Alternativa por divisor de tensión: $V_A = V_{CC} \cdot \frac{R_A}{R_1 + R_A} = 24 \cdot \frac{764.71}{1234.71} = 14.864\text{ V}$).*

     * **Corrientes en el Nodo A:**
       $$I_{R2} = \frac{V_A}{R_2} = \frac{14.864\text{ V}}{1500\,\Omega} = 9.909\text{ mA}$$
       $$I_{R3} = \frac{V_A}{R_{\text{rama\_derecha}}} = \frac{14.864\text{ V}}{1560\,\Omega} = 9.528\text{ mA}$$
       *Verificación LCK Nodo A:* $I_{total} = 19.438\text{ mA} \approx I_{R2} + I_{R3} = 9.909 + 9.528 = 19.437\text{ mA}$ *(coincidencia con error por redondeo $< 0.01\%$).*

     * **Tensión en el Nodo B ($V_B$):**
       $$V_B = V_A - (I_{R3} \cdot R_3) = 14.864\text{ V} - (9.528\text{ mA} \cdot 680\,\Omega) = 14.864\text{ V} - 6.479\text{ V} = 8.385\text{ V}$$
       *(Alternativa por divisor: $V_B = V_A \cdot \frac{R_{4 \parallel L}}{R_3 + R_{4 \parallel L}} = 14.864 \cdot \frac{880}{1560} = 8.385\text{ V}$).*

     * **Corrientes en el Nodo B:**
       $$I_{R4} = \frac{V_B}{R_4} = \frac{8.385\text{ V}}{1200\,\Omega} = 6.988\text{ mA}$$
       $$I_L = \frac{V_B}{R_L} = \frac{8.385\text{ V}}{3300\,\Omega} = 2.541\text{ mA}$$
       *Verificación LCK Nodo B:* $I_{R3} = 9.528\text{ mA} \approx I_{R4} + I_L = 6.988 + 2.541 = 9.529\text{ mA}$ *(coherencia física total).*

  6. **Paso 6: Balance de Potencias:**
     * Potencia generada por la fuente:
       $$P_{\text{fuente}} = V_{CC} \cdot I_{total} = 24\text{ V} \cdot 19.438\text{ mA} = 466.51\text{ mW}$$
     * Potencias disipadas en cada elemento:
       $$P_{R1} = (19.438\text{ mA})^2 \cdot 470\,\Omega = 177.58\text{ mW}$$
       $$P_{R2} = \frac{(14.864\text{ V})^2}{1500\,\Omega} = 147.29\text{ mW}$$
       $$P_{R3} = (9.528\text{ mA})^2 \cdot 680\,\Omega = 61.73\text{ mW}$$
       $$P_{R4} = \frac{(8.385\text{ V})^2}{1200\,\Omega} = 58.59\text{ mW}$$
       $$P_{RL} = \frac{(8.385\text{ V})^2}{3300\,\Omega} = 21.31\text{ mW}$$
     * Suma de potencias disipadas:
       $$\sum P_R = 177.58 + 147.29 + 61.73 + 58.59 + 21.31 = 466.50\text{ mW} \approx P_{\text{fuente}}$$

---

### 3. 📚 Ficha de Repaso Cornell-Kwik (Para Dominio Rápido)

#### 📋 Ficha Técnica (Estilo Cornell)
| Claves / Preguntas Clave | Detalles Técnicos (Respuestas Directas) |
| :--- | :--- |
| **Concepto / Ley Principal** | Reducción progresiva de topologías combinadas mediante identificación de nodos exclusivos (serie) y pares nodales comunes (paralelo). |
| **Ecuación Fundamental** | $R_{in} = R_{serie} + (R_{derivacion} \parallel R_{siguiente})$, aplicada recursivamente desde la carga hacia la fuente. |
| **Error Común a Evitar** | Asumir que dos resistencias están en serie simplemente porque están dibujadas alineadas, ignorando una derivación intermedia de corriente (nodo esencial intermedio). |
| **Relación con Electrónica I y II** | Determinación de la resistencia de entrada $R_{in}$ en etapas de amplificación multietapa, cálculo del punto $Q$ en redes de polarización con carga y diseño de convertidores DAC R-2R. |

#### 💡 Análisis Creativo (Estilo Kwik)
* **Analogía (Create):** Reducir una red serie-paralelo es como pelar una cebolla o desarmar una muñeca rusa: siempre se empieza por la capa más externa (la carga lejana) combinando hacia el núcleo (la fuente). Si intentas romper la muñeca desde el centro, rompes la estructura de nodos.
* **Duda Crítica (Inquire):** *Si la resistencia de carga $R_L$ se reduce drásticamente (ejemplo: de $3.3\text{ k}\Omega$ a $100\,\Omega$), ¿qué le sucede al voltaje $V_A$ del nodo anterior?* Disminuye. Debido al acoplamiento de la red, una menor $R_L$ disminuye la resistencia equivalente del bloque derecho, aumentando la corriente total de la fuente y la caída de tensión en $R_1$, reduciendo el voltaje $V_A$. Esto demuestra experimentalmente el **efecto de carga** entre etapas.
* **Prueba de Fuego (Apply):** Si en una red escalera de 3 celdas idénticas con $R_{serie} = 1\text{ k}\Omega$ y $R_{shunt} = 2\text{ k}\Omega$, la última celda se termina con una carga $R_L = 2\text{ k}\Omega$, ¿cuál es la resistencia equivalente de la última etapa? ($R_{shunt} \parallel R_L = 2\text{ k}\Omega \parallel 2\text{ k}\Omega = 1\text{ k}\Omega$; y en serie con $R_{serie}$ da exactamente $2\text{ k}\Omega$, reproduciendo la propiedad auto-similar de la escalera infinita).

---

### 4. 🛠️ Herramientas Digitales y Simulación

* **Prompt para Mini App Interactiva (Gemini Canvas / HTML5):**
> *"Genera una aplicación web interactiva en un solo archivo HTML5/JS autocontenido con Tailwind CSS y diseño profesional tipo dashboard de ingeniería electrónica oscura. Debe simular una red resistiva multietapa serie-paralelo compuesta por una fuente $V_{CC}$ (con slider de $5\text{ V}$ a $30\text{ V}$), una resistencia de entrada $R_1$, una rama en derivación $R_2$, una resistencia de acoplamiento $R_3$, una resistencia de carga local $R_4$ y una carga externa conmutable/ajustable $R_L$. La aplicación debe mostrar un esquema SVG dinámico con las corrientes y voltajes sobre cada nodo ($V_A, V_B$), barras de disipación de potencia térmica por componente y una tabla de balance energético en tiempo real que demuestre la ley de conservación de la energía y el efecto de carga al variar $R_L$."*
