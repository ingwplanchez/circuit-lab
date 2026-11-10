# 📌 Día 2 - Lección 2: Divisores de Tensión y Cálculo Rápido de Caídas de Voltaje en Polarización

**Objetivo de Ingeniería / Electrónica:** Dominar el principio del divisor de tensión resistivo tanto en condiciones ideales (a circuito abierto) como en condiciones reales con carga finita ($R_L$), calculando con agilidad y rigor las caídas de voltaje que polarizan terminales de compuerta en MOSFETs y fijan la tensión de base ($V_B$) en amplificadores bipolares (BJT) mediante la condición de "divisor rígido".

**Agenda de Tiempo:**
* **Bloque de estudio enfocado (35 min):** Deducción fundamental a partir de LVK/Ohm, fórmula rápida de proporcionalidad, modelado del efecto de carga resistivo ($R_2 \parallel R_L$), error de regulación porcentual y el criterio de diseño de ingeniería del factor $\times 10$ ($R_L \ge 10 R_2$ o $I_{\text{divisor}} \ge 10 I_B$).

---

### 1. 🖊️ Guión Rápido de Repaso (Diseñado para dominio conceptual veloz)

* **Fundamentos Teóricos & Conexión Electrónica:**
  * Un **divisor de tensión** es una red de dos o más resistencias conectadas en serie a través de una fuente de voltaje. Como la misma corriente atraviesa todos los elementos, la caída de tensión en cada resistencia es estrictamente proporcional a su fracción respecto a la resistencia total del lazo.
  * **El Fenómeno del Efecto de Carga:** La fórmula básica $V_{out} = V_s \frac{R_2}{R_1 + R_2}$ es válida **únicamente si no se drena corriente del nodo de salida** ($I_L = 0$ o $R_L = \infty$). Cuando se conecta una carga externa o la entrada de un transistor (por ejemplo, la base de un BJT con impedancia de entrada $R_{in(base)} \approx \beta R_E$), la resistencia efectiva en la parte inferior pasa a ser $R_2 \parallel R_L$. Esto reduce la resistencia neta inferior y colapsa la tensión de salida $V_{out}$.
  * **Conexión con Electrónica I y II:**
    1. **Polarización Universal por Divisor de Tensión en BJT:** Es la topología estándar para estabilizar el punto de reposo $Q$ frente a variaciones del parámetro $\beta$ (por temperatura o sustitución del transistor). Se diseña para que el divisor sea **rígido o firme**, garantizando que $I_{R2} \ge 10 I_B$, lo que hace que $V_B$ dependa solo de las resistencias pasivas y de $V_{CC}$.
    2. **Polarización de Compuerta en MOSFET:** Dado que el óxido de compuerta aísla eléctricamente el terminal ($I_G \approx 0$), la carga es idealmente infinita ($R_{in(gate)} \to \infty$). Por tanto, la tensión de compuerta $V_G$ cumple de forma casi exacta la ecuación ideal de divisor sin carga.
    3. **Atenuadores de Instrumentación y Referencias de ADC:** Los microcontroladores y sensores usan divisores de tensión para adecuar niveles altos (ej. baterías de $12\text{ V}$) a rangos seguros de medición ($0 - 3.3\text{ V}$ o $0 - 5\text{ V}$).

* **Las 3 Fórmulas Esenciales:**
  1. **Divisor de Tensión Ideal (A Circuito Abierto / Sin Carga):**
     $$V_{out\_NL} = V_s \cdot \left( \frac{R_2}{R_1 + R_2} \right) \quad [\text{V}]$$

  2. **Divisor de Tensión Real (Bajo Carga $R_L$):**
     $$V_{out\_L} = V_s \cdot \left( \frac{R_2 \parallel R_L}{R_1 + (R_2 \parallel R_L)} \right) \quad \text{donde } R_2 \parallel R_L = \frac{R_2 \cdot R_L}{R_2 + R_L} \quad [\text{V}]$$

  3. **Regla de Inmunidad al Efecto de Carga (Criterio de Estabilidad 10:1):**

   Para que la impedancia conectada no distorsione el voltaje fijado por el divisor se debe cumplir lo siguiente:
   
     $$R_L \ge 10 \cdot R_2 \iff I_{\text{divisor}} \ge 10 \cdot I_L \quad \implies \quad \% \text{Error} = \frac{V_{out\_NL} - V_{out\_L}}{V_{out\_NL}} \times 100\% \le 9.1\%$$

     

     * **Enfoque de Corriente (Corriente de Polarización vs. Corriente de Carga):** La corriente que circula por la rama del divisor ($I_{\text{polarización}}$ o corriente de sangría / *bleeder*) debe ser al menos 10 veces mayor que la corriente drenada por la carga ($I_L$):
       $$I_{\text{polarización}} \ge 10 \cdot I_L \implies I_{R2} \approx I_{R1}$$

     * **Impacto Numérico en el Error de Tensión:**
       $$\% \text{Error} = \frac{|V_{out\_NL} - V_{out\_L}|}{V_{out\_NL}} \times 100\% \le 9.1\% \approx 10\%$$
       *(Garantiza que la caída de tensión por conectar la carga sea inferior al $10\%$, permitiendo despreciar el efecto de carga en cálculos preliminares de hardware).*


* **Diagrama de Análisis (Divisor Ideal vs Con Carga Acoplada):**

```text
       Divisor Ideal (Sin Carga)                   Divisor Real (Con Carga RL)
       
              + V_CC                                      + V_CC
                │                                           │
              [ R1 ] (Superior)                           [ R1 ] (Superior)
                │                                           │
  Nodo V_out ───o──────► (Abierto: I_L = 0)   Nodo V_out ───o──────────────┐
                │                                           │              │
              [ R2 ] (Inferior)                           [ R2 ]         [ RL ] (Carga)
                │                                           │              │
               GND                                         GND            GND
        V_out = Vcc · R2/(R1+R2)                    V_out = Vcc · (R2||RL) / [R1 + (R2||RL)]
```

* **Estrategia IPEE de Resolución de Problemas (Paso a Paso):**
  1. *Identificar:* Reconocer la fuente de alimentación $V_s$, la resistencia pull-up o superior ($R_1$), la resistencia pull-down o inferior ($R_2$) y la resistencia o impedancia de carga conectada al nodo divisor ($R_L$).
  2. *Plantear:* Determinar si el divisor puede asumirse ideal ($R_L \ge 10 R_2$) o si es obligatorio calcular el paralelo $R_{eq2} = R_2 \parallel R_L$. Escribir la expresión correspondiente de $V_{out}$.
  3. *Ejecutar:* Calcular numéricamente $R_{eq2}$, sustituir en la fórmula del divisor de tensión y determinar las corrientes de cada rama ($I_{R1}, I_{R2}, I_L$).
  4. *Evaluar:* Comprobar que $V_{out} < V_s$. Verificar la conservación de corriente en el nodo central ($I_{R1} = I_{R2} + I_L$) y cuantificar la caída por regulación ($\% \text{Error}$).

---

### 2. 📐 Ejercicio Resuelto Paso a Paso (Enfoque Práctico)

* **Contexto de Electrónica:** Red de polarización universal de base para una etapa amplificadora con transistor BJT NPN en configuración emisor común. La fuente de alimentación continua es $V_{CC} = 15\text{ V}$. Las resistencias del divisor son $R_1 = 33\text{ k}\Omega$ y $R_2 = 10\text{ k}\Omega$. La etapa siguiente presenta una impedancia de entrada de base equivalente de carga $R_L = R_{in(base)} = 47\text{ k}\Omega$.

* **Diagrama Esquemático del Circuito:**

```text
                         + V_CC = 15 V
                              │
                              │ I_total (I_R1)
                              ▼
                         [ R1 = 33 kΩ ]
                              │
          Nodo de Base (VB)   │
           ───────────────────●───────────────────┐
                              │                   │
                              │ I_R2              │ I_B (Hacia la Base)
                              ▼                   ▼
                         [ R2 = 10 kΩ ]      [ RL = Rin(base) = 47 kΩ ]
                              │                   │
                              │                   │
                             ─┴─                 ─┴─
                          GND (0 V)           GND (0 V)
```

* **Desarrollo Numérico Completo:**

  1. **Paso 1: Cálculo del voltaje en vacío / sin carga ($V_{B\_NL}$):**
     Asumiendo inicialmente que la base no drena corriente ($R_L = \infty$):
     $$V_{B\_NL} = V_{CC} \cdot \left( \frac{R_2}{R_1 + R_2} \right) = 15\text{ V} \cdot \left( \frac{10\text{ k}\Omega}{33\text{ k}\Omega + 10\text{ k}\Omega} \right) = 15\text{ V} \cdot \frac{10}{43} \approx 3.488\text{ V}$$

  2. **Paso 2: Evaluación previa del criterio de rigidez del divisor:**
     Verificamos si $R_L \ge 10 \cdot R_2$:
     $$10 \cdot R_2 = 10 \cdot 10\text{ k}\Omega = 100\text{ k}\Omega$$
     Como $R_L = 47\text{ k}\Omega < 100\text{ k}\Omega$, **el divisor NO es rígido**. La corriente drenada por la base de la carga provocará una atenuación apreciable que no se puede ignorar en el diseño.

  3. **Paso 3: Cálculo de la resistencia equivalente inferior bajo carga ($R_{2 \parallel L}$):**
     $$R_{2 \parallel L} = \frac{R_2 \cdot R_L}{R_2 + R_L} = \frac{10\text{ k}\Omega \cdot 47\text{ k}\Omega}{10\text{ k}\Omega + 47\text{ k}\Omega} = \frac{470}{57}\text{ k}\Omega \approx 8.246\text{ k}\Omega$$

  4. **Paso 4: Tensión real de polarización en el nodo de base ($V_{B\_L}$):**
     Aplicando la ecuación del divisor de tensión con la resistencia efectiva $R_{2 \parallel L}$:
     $$V_{B\_L} = V_{CC} \cdot \left( \frac{R_{2 \parallel L}}{R_1 + R_{2 \parallel L}} \right) = 15\text{ V} \cdot \left( \frac{8.246\text{ k}\Omega}{33\text{ k}\Omega + 8.246\text{ k}\Omega} \right) = 15\text{ V} \cdot \frac{8.246}{41.246} \approx 2.999\text{ V} \approx 3.00\text{ V}$$

  5. **Paso 5: Cálculo del error porcentual por efecto de carga:**
     $$\% \text{Error} = \frac{V_{B\_NL} - V_{B\_L}}{V_{B\_NL}} \times 100\% = \frac{3.488\text{ V} - 2.999\text{ V}}{3.488\text{ V}} \times 100\% = \frac{0.489}{3.488} \times 100\% \approx 14.02\%$$
     *(Una reducción de casi $0.5\text{ V}$, suficiente para alterar drásticamente la corriente de reposo $I_C = (V_B - 0.7\text{V})/R_E$ si se hubiese calculado erróneamente sin considerar la carga).*

  6. **Paso 6: Distribución de corrientes en el nodo de base:**
     * Corriente total por la resistencia superior $R_1$:
       $$I_{R1} = \frac{V_{CC} - V_{B\_L}}{R_1} = \frac{15\text{ V} - 2.999\text{ V}}{33\text{ k}\Omega} = \frac{12.001\text{ V}}{33,000\,\Omega} \approx 0.3637\text{ mA} = 363.7\text{ }\mu\text{A}$$
     * Corriente desviada por la resistencia inferior $R_2$:
       $$I_{R2} = \frac{V_{B\_L}}{R_2} = \frac{2.999\text{ V}}{10,000\,\Omega} \approx 0.2999\text{ mA} = 299.9\text{ }\mu\text{A}$$
     * Corriente drenada hacia la base (carga $R_L$):
       $$I_B = I_L = \frac{V_{B\_L}}{R_L} = \frac{2.999\text{ V}}{47,000\,\Omega} \approx 0.0638\text{ mA} = 63.8\text{ }\mu\text{A}$$
     * **Comprobación LCK en el nodo de base:**
       $$I_{R2} + I_L = 299.9\text{ }\mu\text{A} + 63.8\text{ }\mu\text{A} = 363.7\text{ }\mu\text{A} = I_{R1} \quad \checkmark$$

---

### 3. 📚 Ficha de Repaso Cornell-Kwik (Para Dominio Rápido)

#### 📋 Ficha Técnica (Estilo Cornell)
| Claves / Preguntas Clave | Detalles Técnicos (Respuestas Directas) |
| :--- | :--- |
| **Principio / Ley Principal** | Reparto proporcional de tensión en impedancias en serie a corriente constante. |
| **Ecuación Fundamental (Ideal vs Real)** | `V_out(NL) = Vs * R2/(R1+R2)` y `V_out(L) = Vs * (R2||RL) / [R1 + (R2||RL)]`. |
| **Regla del Factor x10 (Rigidez)** | Si $R_L \ge 10 R_2$, la carga drena menos del $10\%$ de la corriente del divisor y el error de voltaje es $< 9.1\%$, permitiendo aproximar $V_{out} \approx V_{out(NL)}$. |
| **Error Típico a Evitar** | Calcular la tensión de base de un BJT o la salida de un atenuador usando la fórmula ideal sin verificar si la carga conectada drena corriente significativa. |
| **Relación con Electrónica I y II** | Polarización universal en transistores BJT ($V_B$), polarización de compuerta en MOSFETs ($V_G$), atenuadores pasivos compensados y referencias fijas para amplificadores operacionales. |

#### 💡 Análisis Creativo (Estilo Kwik)
* **Analogía (Create):** El divisor de tensión ideal es como una cascada con dos estanques en serie: el nivel del estanque inferior depende de la altura relativa de los muros. Conectar una resistencia de carga ($R_L$) es como abrir una tubería de desagüe en el segundo estanque: si el desagüe es grande (baja $R_L$), el nivel del estanque ($V_{out}$) bajará inevitablemente a menos que la corriente de entrada sea enorme.
* **Duda Crítica (Inquire):** *¿Por qué no diseñamos siempre los divisores de polarización con resistencias sumamente pequeñas (ejemplo: $R_1 = 33\,\Omega$ y $R_2 = 10\,\Omega$) para hacerlos 100% inmunes a cualquier carga?* Porque la corriente estática en reposo ($I_{\text{divisor}} = V_{CC}/(R_1 + R_2)$) sería gigantesca ($\approx 350\text{ mA}$), provocando un consumo de potencia excesivo ($P \approx 5.25\text{ W}$), disipación térmica inaceptable y descargando rápidamente baterías en sistemas portátiles. El diseño en ingeniería siempre busca el balance óptimo entre rigidez y bajo consumo.
* **Prueba de Fuego (Apply):** Si $V_s = 10\text{ V}$, $R_1 = 1\text{ k}\Omega$ y $R_2 = 1\text{ k}\Omega$, ¿cuál es $V_{out}$ a circuito abierto? ($5\text{ V}$). Y si conectas una carga idéntica $R_L = 1\text{ k}\Omega$, ¿a cuánto cae $V_{out}$? ($R_2 \parallel R_L = 500\,\Omega \implies V_{out} = 10 \cdot \frac{500}{1000 + 500} = \frac{10}{3} \approx 3.33\text{ V}$, un colapso del $33.3\%$).

---

### 4. 🛠️ Herramientas Digitales y Simulación

* **Prompt para Mini App Interactiva (Gemini Canvas / HTML5):**
> *"Genera una aplicación web interactiva en un solo archivo HTML5/CSS/JS autocontenido con Tailwind CSS y estética oscura de laboratorio electrónico profesional. Debe simular un Divisor de Tensión con Carga Resistiva para Polarización Electrónica. Incluye sliders para ajustar la fuente $V_{CC}$ ($1\text{ V}$ a $30\text{ V}$), la resistencia superior $R_1$ ($100\,\Omega$ a $100\text{ k}\Omega$), la resistencia inferior $R_2$ ($100\,\Omega$ a $100\text{ k}\Omega$) y la resistencia de carga $R_L$ ($100\,\Omega$ a $500\text{ k}\Omega$) con interruptor ON/OFF para alternar entre vacío y carga. La interfaz debe mostrar un esquema SVG dinámico, un medidor visual comparativo que muestre $V_{out}$ en vacío vs $V_{out}$ con carga, el cálculo del error porcentual por regulación de carga ($\% \text{Error}$) y un indicador luminoso que califique la condición de diseño: 'Divisor Rígido / Estable' (verde si $R_L \ge 10 R_2$) o 'Divisor Sensible a Carga' (rojo/ámbar si $R_L < 10 R_2$)."*
