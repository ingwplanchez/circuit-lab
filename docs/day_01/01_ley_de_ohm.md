# 📌 Día 1 - Lección 1: Ley de Ohm y Fundamentos de Resistencia Equivalente

**Objetivo de Ingeniería / Electrónica:** Dominar la relación lineal entre tensión, corriente y resistencia para calcular caídas de tensión estáticas y determinar redes resistivas equivalentes (serie/paralelo) antes de polarizar terminales de diodos o transistores.

**Agenda de Tiempo:**

* **Bloque de estudio enfocado (30 min):** Concepto físico de resistencia, formulación de la Ley de Ohm, potencia disipada y reducción serie-paralelo.

---

### 1. 🖊️ Guión Rápido de Repaso (Diseñado para dominio conceptual veloz)

* **Fundamentos Teóricos & Conexión Electrónica:**
* La **Ley de Ohm** establece que la corriente $I$ que fluye a través de un material conductor lineal es directamente proporcional a la tensión $V$ aplicada e inversamente proporcional a su resistencia $R$. En Electrónica I y II, esta ley es omnipresente: se utiliza para calcular las resistencias de polarización de base en transistores BJT, determinar las resistencias de limitación en diodos LED o calcular el punto de operación estático en divisores resistivos.
* La **Resistencia Equivalente ($R_{eq}$)** permite simplificar redes complejas de componentes pasivos en configuraciones serie y paralelo para reducir el circuito a una sola impedancia de carga vista desde una fuente de alimentación.


* **Las 3 Fórmulas Esenciales:**
1. **Ley de Ohm (Voltaje):**

$$V = I \cdot R \quad \text{[Volts, V]}$$


2. **Disipación de Potencia:**

$$P = V \cdot I = I^2 \cdot R = \frac{V^2}{R} \quad \text{[Watts, W]}$$


3. **Resistencia Equivalente (Serie vs Paralelo):**
* Serie: $R_{eq} = R_1 + R_2 + \dots + R_n$
* Paralelo (dos ramas): $R_{eq} = \frac{R_1 \cdot R_2}{R_1 + R_2}$




* **Diagrama de Análisis (Esquema Visual de Red Serie-Paralelo):**

```text
       +----[ R2 ]----+
       |              |
--[Vs]-+----[ R3 ]----+--[ R1 ]-- (Nodo de Carga)
       |              |
       +----[ R4 ]----+

```

* **Estrategia IPEE de Resolución de Problemas (Paso a Paso):**
1. *Identificar:* Reconocer qué elementos están estrictamente en serie (misma corriente) y cuáles en paralelo (mismo voltaje).
2. *Plantear:* Agrupar algebraicamente las resistencias desde la más lejana a la fuente hacia la fuente principal utilizando las fórmulas de $R_{eq}$.
3. *Ejecutar:* Calcular la corriente total entregada por la fuente mediante la Ley de Ohm general ($I_{total} = V_s / R_{eq}$).
4. *Evaluar:* Comprobar que la potencia entregada por la fuente de voltaje coincida exactamente con la suma de las potencias individuales disipadas por cada resistencia ($P_{s} = \sum P_{Ri}$).



---

### 2. 📐 Ejercicio Resuelto Paso a Paso (Enfoque Práctico)

* **Contexto de Electrónica:** Diseño preliminar de una red de alimentación auxiliar para un circuito integrado que requiere limitar una corriente de entrada a partir de una fuente de CD de $15\text{ V}$.
* **Enunciado del Problema:**
Dado un circuito con una fuente de tensión continua $V_s = 15\text{ V}$, se conecta una malla que contiene una resistencia en serie $R_1 = 330\,\Omega$ y un arreglo en paralelo de dos resistencias: $R_2 = 1.2\text{ k}\Omega$ y $R_3 = 2.2\text{ k}\Omega$. Calcule la resistencia equivalente total del circuito, la corriente total suministrada por la fuente y la potencia disipada por la resistencia $R_1$.

* **Diagrama Esquemático del Circuito:**

```text
               Itotal --->
         ┌───────────[ R1 = 330 Ω ]───────────┬────────────────┐
         │                                    │                │
       + │                                    │                │
     ( Vs = 15 V )                        [ R2 = 1.2 kΩ ]  [ R3 = 2.2 kΩ ]
       - │                                    │                │
         │                                    │                │
         └────────────────────────────────────┴────────────────┘
```

* **Desarrollo Numérico Completo:**
1. *Paso 1 (Identificar y simplificar el paralelo de $R_2$ y $R_3$):*

$$R_{23} = \frac{R_2 \cdot R_3}{R_2 + R_3} = \frac{(1200\,\Omega) \cdot (2200\,\Omega)}{1200\,\Omega + 2200\,\Omega} = \frac{2,640,000}{3400} \approx 776.47\,\Omega$$


2. *Paso 2 (Calcular la resistencia equivalente total $R_{eq}$ en serie con $R_1$):*

$$R_{eq} = R_1 + R_{23} = 330\,\Omega + 776.47\,\Omega = 1106.47\,\Omega \approx 1.106\text{ k}\Omega$$


3. *Paso 3 (Ejecutar cálculo de corriente total con la Ley de Ohm):*

$$I_{total} = \frac{V_s}{R_{eq}} = \frac{15\text{ V}}{1106.47\,\Omega} \approx 0.01356\text{ A} = 13.56\text{ mA}$$


4. *Paso 4 (Evaluar potencia disipada en $R_1$):*

$$P_{R1} = (I_{total})^2 \cdot R_1 = (0.01356\text{ A})^2 \cdot 330\,\Omega \approx 0.0606\text{ W} = 60.6\text{ mW}$$



*(Verificación: El valor de potencia está muy por debajo del límite estándar de $1/4\text{ W}$, por lo que el diseño físico resistivo es seguro).*



---

### 3. 📚 Ficha de Repaso Cornell-Kwik (Para Dominio Rápido)

#### 📋 Ficha Técnica (Estilo Cornell)

| Claves / Preguntas Clave | Detalles Técnicos (Respuestas Directas) |
| --- | --- |
| **Concepto / Ley Principal** | Proporcionalidad directa entre tensión e intensidad mediada por la oposición resistiva. |
| **Ecuación Fundamental** | `V = I * R` y `P = I^2 * R` |
| **Error Común a Evitar** | Sumar resistencias en paralelo como si estuvieran en serie, o mezclar unidades de Ohmios con kilo-ohmios en las ecuaciones de potencia. |
| **Relación con Electrónica I y II** | Imprescindible para dimensionar resistencias colectoras, emisoras y de polarización de base en transistores. |

#### 💡 Análisis Creativo (Estilo Kwik)

* **Analogía (Create):** La resistencia es como un embudo en una tubería: cuanto más estrecho es el cuello (mayor resistencia), menor es el caudal de agua (corriente) que pasa para una misma presión (voltaje).
* **Duda Crítica (Inquire):** *¿Qué ocurre con la resistencia equivalente si colocamos una resistencia de valor extremadamente pequeño en paralelo con otra mucho mayor?* La resistencia equivalente resultante siempre tenderá a ser ligeramente menor que la resistencia más pequeña del arreglo paralelo.
* **Prueba de Fuego (Apply):** Si cruzan $5\text{ mA}$ por una resistencia de $2\text{ k}\Omega$, ¿cuál es la caída de tensión? ($V = 5 \times 10^{-3} \times 2000 = 10\text{ V}$).

---

### 4. 🛠️ Herramientas Digitales y Simulación

* **Prompt para Mini App Interactiva (Gemini Canvas / HTML5):**
> *"Genera una aplicación web interactiva en un solo archivo HTML/JS autocontenido que permita simular un circuito resistivo serie-paralelo compuesto por una fuente de voltaje de $12\text{V}$, una resistencia principal $R_1$ y dos resistencias en paralelo $R_2$ y $R_3$. La interfaz debe incluir controles deslizantes (*sliders*) para modificar los valores de $R_1$ ($100\,\Omega \text{ a } 1\text{k}\Omega$), $R_2$ y $R_3$, y actualizar de forma instantánea y dinámica la resistencia equivalente total, la corriente de la fuente y la potencia disipada en cada componente con indicadores visuales de barra."*



