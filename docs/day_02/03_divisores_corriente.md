# 📌 Día 2 - Lección 3: Divisores de Corriente para el Reparto de Intensidades en Mallas Adyacentes

**Objetivo de Ingeniería / Electrónica:** Dominar el principio del divisor de corriente resistivo en redes paralelas multirama tanto por la fórmula dual cruzada (dos ramas) como por el método de conductancias ($N$ ramas), capacitándose para calcular con rapidez la derivación de intensidades en mallas adyacentes, espejos de corriente con transistores y derivaciones (*shunts*) en etapas de potencia y sensado.

**Agenda de Tiempo:**
* **Bloque de estudio enfocado (35 min):** Deducción fundamental a partir de LCK/Ohm, fórmula dual de la resistencia opuesta ($I_k \propto R_{\text{opuesta}}$), formulación general por conductancias ($G_k / G_{total}$), balance energético y aplicación en circuitos integrados (espejos de corriente y etapas de polarización diferencial).

---

### 1. 🖊️ Guión Rápido de Repaso (Diseñado para dominio conceptual veloz)

* **Fundamentos Teóricos & Conexión Electrónica:**
  * Un **divisor de corriente** es una red de dos o más elementos pasivos conectados en paralelo a través de un nodo común alimentado por una corriente total $I_{total}$. Debido a que todas las ramas en paralelo comparten exactamente la misma caída de tensión ($V_p$), la corriente total se bifurca inversamente proporcional a la resistencia de cada rama: **la rama de menor resistencia absorbe la mayor fracción de corriente**.
  * **Dualidad Fundamental con el Divisor de Tensión:**
    * En el divisor de tensión (elementos en serie), el voltaje en $R_1$ es proporcional a su propia resistencia: $V_1 = V_s \frac{R_1}{R_1 + R_2}$.
    * En el divisor de corriente (elementos en paralelo de dos ramas), la corriente en $R_1$ es proporcional a la resistencia de la **otra** rama: $I_1 = I_{total} \frac{R_2}{R_1 + R_2}$.
  * **Conexión con Electrónica I y II:**
    1. **Espejos y Fuentes de Corriente:** En circuitos integrados analógicos (como los amplificadores operacionales 741 o pares diferenciales CMOS/BJT), las corrientes de polarización de las etapas activas se distribuyen a través de redes divisoras de corriente resistivas fijadas por transistores acoplados.
    2. **Resistencias Shunt de Censado y Protección:** En fuentes conmutadas (SMPS) y controladores de motores mecatrónicos, se coloca una resistencia muy baja en paralelo para derivar una fracción conocida de corriente hacia un circuito amplificador de censado.
    3. **Pares Diferenciales:** La corriente de cola ($I_{tail}$) se reparte entre los dos transistores del par en función de la conductancia dinámica de sus respectivos canales o uniones base-emisor.

* **Las 3 Fórmulas Esenciales:**
  1. **Divisor de Corriente para Dos Ramas en Paralelo (Regla Cruzada):**
     $$I_1 = I_{total} \cdot \left( \frac{R_2}{R_1 + R_2} \right) \quad \text{y} \quad I_2 = I_{total} \cdot \left( \frac{R_1}{R_1 + R_2} \right) \quad [\text{A}]$$

  2. **Divisor de Corriente General para $N$ Ramas (Formulación por Conductancias):**
     $$I_k = I_{total} \cdot \left( \frac{G_k}{G_{total}} \right) = I_{total} \cdot \left( \frac{\frac{1}{R_k}}{\sum_{j=1}^N \frac{1}{R_j}} \right) \quad [\text{A}]$$

  3. **Tensión de Nodo Común en Paralelo:**
     $$V_p = I_{total} \cdot R_p = I_1 R_1 = I_2 R_2 = \dots = I_N R_N \quad \text{donde } R_p = \frac{1}{\sum \frac{1}{R_j}} \quad [\text{V}]$$

* **Diagrama de Análisis (Bifurcación de Corriente en Nodo Común):**

```text
                  Nodo Común Superior (V_p)
                  ●───────────────────┬───────────────────┐
                  │                   │                   │
               ▲  │                   │                   │
    I_total   (↑) │ I_1               │ I_2               │ I_3
   (o Fuente)  │  ▼                   ▼                   ▼
                  │              [ R2 = 1.2 kΩ ]     [ R3 = 2.2 kΩ ]
             [ R1 = 680 Ω ]           │                   │
                  │                   │                   │
                  │                   │                   │
                  ●───────────────────┴───────────────────┘
                  Nodo Común Inferior (GND = 0 V)

       Regla: La rama de 680 Ω (menor R) drena la corriente más alta.
```

* **Estrategia IPEE de Resolución de Problemas (Paso a Paso):**
  1. *Identificar:* Localizar el nodo de entrada por donde ingresa la corriente total $I_{total}$ y reconocer las ramas que están estrictamente en paralelo (conectadas entre el mismo par de nodos).
  2. *Plantear:*
     * Si son **dos ramas**, aplicar directamente la fórmula cruzada: $I_1 = I_{total} \frac{R_2}{R_1 + R_2}$.
     * Si son **tres o más ramas**, calcular las conductancias individuales ($G_k = 1/R_k$) y la conductancia total ($G_T = \sum G_k$), o bien hallar la tensión común $V_p = I_{total} \cdot R_{eq\_paralelo}$ y luego aplicar la Ley de Ohm en cada rama ($I_k = V_p / R_k$).
  3. *Ejecutar:* Realizar las operaciones numéricas con unidades coherentes (mA, A, $\Omega$, k$\Omega$).
  4. *Evaluar:* Comprobar rigurosamente la Ley de Corrientes de Kirchhoff en el nodo: $\sum I_{\text{ramas}} = I_{total}$. Verificar que la rama de menor resistencia tenga efectivamente la mayor corriente.

---

### 2. 📐 Ejercicio Resuelto Paso a Paso (Enfoque Práctico)

* **Contexto de Electrónica:** Etapa de distribución de corriente para la polarización de una rama de protección activa y un par diferencial. Una fuente de corriente constante integrada suministra $I_{total} = 12\text{ mA}$. Esta corriente entra a un nodo que alimenta tres ramas en paralelo:
  * Rama 1: Resistencia limitadora de censado $R_1 = 470\,\Omega$.
  * Rama 2: Resistencia de polarización del par $R_2 = 1.2\text{ k}\Omega = 1200\,\Omega$.
  * Rama 3: Resistencia de estabilización térmica $R_3 = 2.2\text{ k}\Omega = 2200\,\Omega$.

* **Diagrama Esquemático del Circuito:**

```text
                                Nodo Superior (V_p)
                  ───────────────●───────────────┬───────────────┐
                  ▲              │               │               │
                  │              │               │               │
            (↑) I_total = 12 mA  ▼ I_1           ▼ I_2           ▼ I_3
                  │              │               │               │
                  │         [ R1 = 470 Ω ]  [ R2 = 1.2 kΩ ] [ R3 = 2.2 kΩ ]
                  │              │               │               │
                  │              │               │               │
                  ───────────────●───────────────┴───────────────┘
                                Nodo Inferior (GND = 0 V)
```

* **Desarrollo Numérico Completo:**

  1. **Paso 1: Cálculo de las conductancias de cada rama ($G_k = 1/R_k$):**
     * Conductancia Rama 1:
       $$G_1 = \frac{1}{470\,\Omega} \approx 2.12766 \times 10^{-3}\text{ S} = 2.12766\text{ mS}$$
     * Conductancia Rama 2:
       $$G_2 = \frac{1}{1200\,\Omega} \approx 0.83333 \times 10^{-3}\text{ S} = 0.83333\text{ mS}$$
     * Conductancia Rama 3:
       $$G_3 = \frac{1}{2200\,\Omega} \approx 0.45455 \times 10^{-3}\text{ S} = 0.45455\text{ mS}$$

  2. **Paso 2: Conductancia total del arreglo paralelo ($G_{total}$):**
     $$G_{total} = G_1 + G_2 + G_3 = 2.12766\text{ mS} + 0.83333\text{ mS} + 0.45455\text{ mS} \approx 3.41554\text{ mS}$$

  3. **Paso 3: Resistencia equivalente en paralelo ($R_p$):**
     $$R_p = \frac{1}{G_{total}} = \frac{1}{3.41554 \times 10^{-3}\text{ S}} \approx 292.78\,\Omega$$

  4. **Paso 4: Tensión común en el nodo paralelo ($V_p$):**
     $$V_p = I_{total} \cdot R_p = 12\text{ mA} \times 292.78\,\Omega = 0.012\text{ A} \times 292.78\,\Omega \approx 3.5134\text{ V}$$

  5. **Paso 5: Reparto de corrientes individuales por divisor:**
     * **Corriente en la Rama 1 ($I_1$):**
       $$I_1 = I_{total} \cdot \left( \frac{G_1}{G_{total}} \right) = 12\text{ mA} \cdot \left( \frac{2.12766}{3.41554} \right) \approx 12\text{ mA} \cdot 0.62294 \approx 7.475\text{ mA}$$
       *(Verificación por Ley de Ohm directa: $I_1 = \frac{V_p}{R_1} = \frac{3.5134\text{ V}}{470\,\Omega} \approx 7.475\text{ mA}$).*

     * **Corriente en la Rama 2 ($I_2$):**
       $$I_2 = I_{total} \cdot \left( \frac{G_2}{G_{total}} \right) = 12\text{ mA} \cdot \left( \frac{0.83333}{3.41554} \right) \approx 12\text{ mA} \cdot 0.24400 \approx 2.928\text{ mA}$$
       *(Verificación por Ley de Ohm directa: $I_2 = \frac{V_p}{R_2} = \frac{3.5134\text{ V}}{1200\,\Omega} \approx 2.928\text{ mA}$).*

     * **Corriente en la Rama 3 ($I_3$):**
       $$I_3 = I_{total} \cdot \left( \frac{G_3}{G_{total}} \right) = 12\text{ mA} \cdot \left( \frac{0.45455}{3.41554} \right) \approx 12\text{ mA} \cdot 0.13308 \approx 1.597\text{ mA}$$
       *(Verificación por Ley de Ohm directa: $I_3 = \frac{V_p}{R_3} = \frac{3.5134\text{ V}}{2200\,\Omega} \approx 1.597\text{ mA}$).*

  6. **Paso 6: Evaluación y Comprobación de LCK y Potencias:**
     * Suma de corrientes de rama:
       $$I_1 + I_2 + I_3 = 7.475\text{ mA} + 2.928\text{ mA} + 1.597\text{ mA} = 12.000\text{ mA} = I_{total} \quad \checkmark$$
     * Porcentaje de corriente absorbido por cada rama:
       * Rama 1 ($470\,\Omega$): **$62.29\%$** de la corriente total.
       * Rama 2 ($1.2\text{ k}\Omega$): **$24.40\%$** de la corriente total.
       * Rama 3 ($2.2\text{ k}\Omega$): **$13.31\%$** de la corriente total.
     * Potencia suministrada por la fuente de corriente:
       $$P_{\text{fuente}} = V_p \cdot I_{total} = 3.5134\text{ V} \times 12\text{ mA} \approx 42.16\text{ mW}$$
     * Potencias disipadas por cada resistor:
       $$P_{R1} = (7.475\text{ mA})^2 \cdot 470\,\Omega \approx 26.26\text{ mW}$$
       $$P_{R2} = (2.928\text{ mA})^2 \cdot 1200\,\Omega \approx 10.29\text{ mW}$$
       $$P_{R3} = (1.597\text{ mA})^2 \cdot 2200\,\Omega \approx 5.61\text{ mW}$$
       $$\sum P_R = 26.26 + 10.29 + 5.61 = 42.16\text{ mW} = P_{\text{fuente}} \quad \checkmark$$

---

### 3. 📚 Ficha de Repaso Cornell-Kwik (Para Dominio Rápido)

#### 📋 Ficha Técnica (Estilo Cornell)
| Claves / Preguntas Clave | Detalles Técnicos (Respuestas Directas) |
| :--- | :--- |
| **Principio Fundamental** | Reparto de corriente inversamente proporcional a la resistencia a tensión idéntica ($I \propto 1/R$). |
| **Fórmula Cruzada (2 ramas)** | $I_1 = I_T \cdot \frac{R_2}{R_1 + R_2}$ y $I_2 = I_T \cdot \frac{R_1}{R_1 + R_2}$. En el numerador va la resistencia de la **otra rama**. |
| **Fórmula General ($N$ ramas)** | $I_k = I_T \cdot \frac{G_k}{G_T} = \frac{V_p}{R_k}$ donde $V_p = I_T / \sum(1/R_j)$. |
| **Error Típico a Evitar** | Poner la resistencia propia en el numerador para dos ramas (confusión con el divisor de tensión) o aplicar la fórmula cruzada de 2 ramas a circuitos de 3 o más ramas sin combinarlas previamente. |
| **Relación con Electrónica I y II** | Espejos de corriente bipolares y MOS, derivaciones de protección en convertidores DC-DC, balance en pares diferenciales y atenuadores de corriente en transconductancia. |

#### 💡 Análisis Creativo (Estilo Kwik)
* **Analogía (Create):** El divisor de corriente es como una autopista de tráfico que se divide en varios caminos paralelos: la mayoría de los vehículos (electrones) elegirá la ruta asfaltada de 8 carriles y baja resistencia ($R_1$ pequeña), mientras que solo un puñado tomará el camino de tierra estrecho y lleno de baches de alta resistencia ($R_3$ grande).
* **Duda Crítica (Inquire):** *¿Por qué NO se puede usar la fórmula $I_1 = I_{total} \cdot \frac{R_2 + R_3}{R_1 + R_2 + R_3}$ para 3 ramas?* Porque la resistencia equivalente de un arreglo paralelo no es la suma de las otras ramas. La física del paralelo responde a la suma de **conductancias** ($1/R_p = 1/R_1 + 1/R_2 + 1/R_3$). La regla cruzada solo funciona matemáticamente cuando el denominador es la suma simple de dos elementos porque $(R_1 \parallel R_2) / R_1 = R_2 / (R_1 + R_2)$. Para $\ge 3$ ramas, el método de conductancias o el cálculo previo de $V_p$ es obligatorio.
* **Prueba de Fuego (Apply):** Si entran $10\text{ mA}$ a un nodo con dos resistencias en paralelo de $R_1 = 1\text{ k}\Omega$ y $R_2 = 9\text{ k}\Omega$, ¿cuánta corriente pasa por $R_1$?
  *Respuesta:* $I_1 = 10\text{ mA} \times \frac{9\text{ k}\Omega}{1\text{ k}\Omega + 9\text{ k}\Omega} = 10 \times \frac{9}{10} = \mathbf{9\text{ mA}}$. Como $R_1$ es 9 veces menor que $R_2$, absorbe exactamente 9 veces más corriente.

---

### 4. 🛠️ Herramientas Digitales y Simulación

* **Prompt para Mini App Interactiva (Gemini Canvas / HTML5):**
> *"Genera una aplicación web interactiva en un solo archivo HTML5/CSS/JS autocontenido con Tailwind CSS y diseño profesional de instrumentación electrónica en modo oscuro. Debe simular un Divisor de Corriente Multirama con una fuente de corriente ajustable $I_{total}$ ($1\text{ mA}$ a $50\text{ mA}$), dos ramas obligatorias $R_1$ y $R_2$ ($50\,\Omega$ a $5\text{ k}\Omega$) y una tercera rama opcional $R_3$ que se pueda activar o desactivar con un interruptor. La interfaz debe incluir un esquema SVG dinámico con flechas animadas proporcionales al flujo de corriente en cada rama, un medidor de porcentajes de reparto de corriente ($I_1\%, I_2\%, I_3\%$), el cálculo de la tensión nodal común $V_p$ y una barra de balance energético que confirme que $\sum I_{\text{ramas}} = I_{total}$."*
