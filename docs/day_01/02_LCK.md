# 📌 Día 1 - Lección 2: Ley de Corrientes de Kirchhoff (LCK) y Conservación de la Carga

**Objetivo de Ingeniería / Electrónica:** Dominar la conservación de la carga en nodos eléctricos para determinar el reparto de corrientes en divisorios y nodos de entrada/salida de etapas activas (como la unión de corrientes de base, colector y emisor en transistores BJT).

**Agenda de Tiempo:**

* **Bloque de estudio enfocado (45 min):** Definición de nodo fundamental, principio de conservación de la carga, formulación algebraica de la LCK y análisis de nodos con fuentes de corriente.

---

### 1. 🖊️ Guión Rápido de Repaso (Diseñado para dominio conceptual veloz)

* **Fundamentos Teóricos & Conexión Electrónica:**
* La **Ley de Corrientes de Kirchhoff (LCK)** es una consecuencia directa del principio físico de **conservación de la carga eléctrica**: la carga no se crea ni se destruye en un punto o nodo de conexión.
* Un **nodo** es la intersección de dos o más ramas de un circuito. La suma algebraica de todas las corrientes que entran a un nodo debe ser estrictamente igual a la suma de todas las corrientes que salen de él.
* **Conexión con Electrónica I y II:** La LCK es la herramienta fundamental para analizar el comportamiento estático y dinámico de los dispositivos semiconductores. Por ejemplo, en un transistor de unión bipolar (BJT), la relación de corrientes que define su operación es una aplicación directa de LCK en el nodo del componente: $I_E = I_B + I_C$. De igual manera, se aplica para analizar los nodos de sumatorio en amplificadores operacionales (Op-Amps).


* **Las 3 Fórmulas Esenciales:**
1. **LCK en Forma General (Entradas vs Salidas):**

$$\sum I_{\text{entrantes}} = \sum I_{\text{salientes}}$$


2. **LCK en Forma Sumatoria Algebraica:**

$$\sum_{k=1}^{N} I_k = 0 \quad \text{(asignando signo + a las entrantes y - a las salientes)}$$


3. **Corriente de Nodo por Ley de Ohm (Expresión en función de Tensiones):**

$$I_{ab} = \frac{V_a - V_b}{R_{ab}}$$




* **Diagrama de Análisis (Esquema Visual de Un Nodo Principal):**

```text
           I1 (Entra)
               │
               ▼
   I2        ┌───┐        I3
(Entra) ───► │ N │ ───► (Sale)
             └───┘
               │
               ▼
           I4 (Sale)

   Ecuación LCK: I1 + I2 = I3 + I4

```

* **Estrategia IPEE de Resolución de Problemas (Paso a Paso):**
1. *Identificar:* Localizar todos los nodos esenciales del circuito (puntos donde se unen 3 o más conductores) y definir un nodo de referencia o masa (Tierra = $0\text{ V}$).
2. *Plantear:* Asignar direcciones arbitrarias de corriente para cada rama conectada al nodo seleccionado.
3. *Ejecutar:* Escribir la ecuación sumatoria $\sum I_{\text{entrantes}} = \sum I_{\text{salientes}}$ en función de los voltajes del nodo usando la expresión $I = (V_{\text{inicio}} - V_{\text{fin}})/R$.
4. *Evaluar:* Resolver algebraicamente la ecuación y verificar los signos. Si una corriente resulta negativa, significa que su flujo real es exactamente opuesto al sentido asumido.



---

### 2. 📐 Ejercicio Resuelto Paso a Paso (Enfoque Práctico y directo)

* **Contexto de Electrónica:** Determinación de la corriente de disparo en un punto de polarización resistivo donde se interconectan dos etapas de amplificación.
* **Enunciado del Problema:**
Considere un nodo principal $N_1$ en un circuito de CD al cual están conectadas tres ramas resistivas y una fuente de corriente independiente:
* Rama 1: Proviene de un voltaje $V_A = 12\text{ V}$ a través de una resistencia $R_1 = 2\text{ k}\Omega$.
* Rama 2: Se conecta a tierra ($0\text{ V}$) mediante una resistencia $R_2 = 4\text{ k}\Omega$.
* Rama 3: Se conecta a un voltaje de referencia $V_B = 3\text{ V}$ mediante una resistencia $R_3 = 1\text{ k}\Omega$.
* Rama 4: Una fuente de corriente constante $I_s = 1.5\text{ mA}$ inyecta corriente directamente hacia el nodo $N_1$.


*Calcule el voltaje $V_{N1}$ en el nodo principal y determine la magnitud y sentido real de la corriente que fluye por la resistencia $R_3$.*

* **Diagrama Esquemático del Circuito:**

```text
                                      ▲
                                     (↑) Is = 1.5 mA
                                      │
                                      │ Is (Entra)
                                      ▼
  VA = 12 V       I1 --->       Nodo N1 (VN1)       I3 --->       VB = 3 V
    (○)──────[ R1 = 2 kΩ ]────────────●────────────[ R3 = 1 kΩ ]──────(○)
                                      │
                                      │ I2 (Sale)
                                      ▼
                                [ R2 = 4 kΩ ]
                                      │
                                     ─┴─
                                  GND (0 V)
```

* **Desarrollo Numérico Completo:**
1. *Paso 1 (Identificar y definir corrientes que entran/salen de $N_1$):*
* Asumimos que la corriente de $V_A$ entra al nodo: $I_1 = \frac{12 - V_{N1}}{2\text{ k}\Omega}$.
* La fuente de corriente entra al nodo: $I_s = 1.5\text{ mA}$.
* Asumimos que la corriente hacia Tierra sale del nodo: $I_2 = \frac{V_{N1} - 0}{4\text{ k}\Omega}$.
* Asumimos que la corriente hacia $V_B$ sale del nodo: $I_3 = \frac{V_{N1} - 3}{1\text{ k}\Omega}$.


2. *Paso 2 (Plantear la ecuación de LCK en el nodo $N_1$):*

$$\sum I_{\text{entrantes}} = \sum I_{\text{salientes}} \implies I_1 + I_s = I_2 + I_3$$


$$\frac{12 - V_{N1}}{2} + 1.5 = \frac{V_{N1}}{4} + \frac{V_{N1} - 3}{1} \quad \text{(con } R \text{ en } k\Omega \text{ e } I \text{ en } mA\text{)}$$


3. *Paso 3 (Ejecutar el despeje de $V_{N1}$):*
Multiplicamos toda la ecuación por $4$ para eliminar denominadores:

$$2(12 - V_{N1}) + 4(1.5) = V_{N1} + 4(V_{N1} - 3)$$


$$24 - 2V_{N1} + 6 = V_{N1} + 4V_{N1} - 12$$


$$30 - 2V_{N1} = 5V_{N1} - 12$$


$$30 + 12 = 5V_{N1} + 2V_{N1} \implies 42 = 7V_{N1}$$


$$V_{N1} = \frac{42}{7} = 6\text{ V}$$


4. *Paso 4 (Evaluar la corriente $I_3$ en la resistencia $R_3$):*

$$I_3 = \frac{V_{N1} - V_B}{R_3} = \frac{6\text{ V} - 3\text{ V}}{1\text{ k}\Omega} = \frac{3\text{ V}}{1\text{ k}\Omega} = 3\text{ mA}$$



*Interpretación:* Puesto que $I_3$ dio un resultado positivo (+3 mA), la dirección asumida originalmente (saliendo de $N_1$ hacia $V_B$) es la correcta.

---

#### Resolución con Estrategia IPEE (Algebraica)

##### 1. Identificar (Leyes aplicables, datos e incógnitas)
* **Leyes Físicas:** Ley de Corrientes de Kirchhoff ($\text{LCK}$) aplicada al nodo $N_1$ y Ley de Ohm expresada en términos de tensiones de nodo.
* **Nodo de Referencia:** Masa/Tierra ($\text{GND} = 0\text{ V}$).
* **Parámetros Conocidos:**
  * Tensiones de frontera: $V_A = 12\text{ V}$, $V_B = 3\text{ V}$, $V_{\text{GND}} = 0\text{ V}$.
  * Resistencias de rama: $R_1 = 2\text{ k}\Omega$, $R_2 = 4\text{ k}\Omega$, $R_3 = 1\text{ k}\Omega$.
  * Fuente de corriente inyectada: $I_s = 1.5\text{ mA}$.
* **Incógnitas:**
  * Voltaje nodal $V_{N1}$.
  * Corriente de rama $I_3$ (magnitud y sentido real a través de $R_3$).

---

##### 2. Plantear (Ecuaciones algebraicas simbólicas)
1. **Balance de Corrientes en el Nodo $N_1$ (LCK):**
   Conforme al diagrama esquemático, definimos las direcciones de corriente:
   * **Entran al nodo:** $I_1$ e $I_s$.
   * **Salen del nodo:** $I_2$ e $I_3$.

   $$\sum I_{\text{entrantes}} = \sum I_{\text{salientes}} \implies I_1 + I_s = I_2 + I_3$$

2. **Expresión de Corrientes de Rama por Ley de Ohm ($I = \frac{V_{\text{inicio}} - V_{\text{fin}}}{R}$):**
   * Corriente desde $V_A$ hacia $N_1$:
     $$I_1 = \frac{V_A - V_{N1}}{R_1}$$
   * Corriente desde $N_1$ hacia $\text{GND}$:
     $$I_2 = \frac{V_{N1} - 0}{R_2} = \frac{V_{N1}}{R_2}$$
   * Corriente desde $N_1$ hacia $V_B$:
     $$I_3 = \frac{V_{N1} - V_B}{R_3}$$

3. **Ecuación Nodal General Simbólica:**
   Sustituyendo cada expresión en la LCK:
   $$\frac{V_A - V_{N1}}{R_1} + I_s = \frac{V_{N1}}{R_2} + \frac{V_{N1} - V_B}{R_3}$$

---

##### 3. Ejecutar (Despeje algebraico y sustitución numérica)

* **Fase A: Despeje Algebraico de $V_{N1}$ (Forma Simbólica Pura):**
  Separamos los términos con la incógnita $V_{N1}$ hacia el miembro derecho y las fuentes hacia el miembro izquierdo:

  $$\frac{V_A}{R_1} - \frac{V_{N1}}{R_1} + I_s = \frac{V_{N1}}{R_2} + \frac{V_{N1}}{R_3} - \frac{V_B}{R_3}$$

  $$\frac{V_A}{R_1} + \frac{V_B}{R_3} + I_s = V_{N1} \left( \frac{1}{R_1} + \frac{1}{R_2} + \frac{1}{R_3} \right)$$

  Despejando $V_{N1}$:
  $$V_{N1} = \frac{\dfrac{V_A}{R_1} + \dfrac{V_B}{R_3} + I_s}{\dfrac{1}{R_1} + \dfrac{1}{R_2} + \dfrac{1}{R_3}}$$

* **Fase B: Sustitución de Valores Conocidos:**
  * *Términos de fuentes (corrientes de excitación en el numerador):*
    $$\frac{V_A}{R_1} = \frac{12\text{ V}}{2\text{ k}\Omega} = 6.0\text{ mA}$$
    $$\frac{V_B}{R_3} = \frac{3\text{ V}}{1\text{ k}\Omega} = 3.0\text{ mA}$$
    $$I_s = 1.5\text{ mA}$$
    $$\text{Numerador} = 6.0\text{ mA} + 3.0\text{ mA} + 1.5\text{ mA} = 10.5\text{ mA}$$

  * *Términos de conductancias en eldenominador  (Siemens = ohm \({}^{-1}\) (\(\Omega ^{-1}\)) o mho ):*
    $$\frac{1}{R_1} = \frac{1}{2\text{ k}\Omega} = 0.5\text{ mS}$$
    $$\frac{1}{R_2} = \frac{1}{4\text{ k}\Omega} = 0.25\text{ mS}$$
    $$\frac{1}{R_3} = \frac{1}{1\text{ k}\Omega} = 1.0\text{ mS}$$
    $$\text{Denominador} = 0.5\text{ mS} + 0.25\text{ mS} + 1.0\text{ mS} = 1.75\text{ mS}$$

  * *Cálculo del Voltaje Nodal $V_{N1}$:*
    $$V_{N1} = \frac{10.5\text{ mA}}{1.75\text{ mS}} = \frac{10.5 \times 10^{-3}\text{ A}}{1.75 \times 10^{-3}\ \Omega^{-1}} = 6.0\text{ V}$$

* **Fase C: Cálculo de la Corriente $I_3$ en $R_3$:**
  $$I_3 = \frac{V_{N1} - V_B}{R_3} = \frac{6.0\text{ V} - 3.0\text{ V}}{1\text{ k}\Omega} = \frac{3.0\text{ V}}{1\text{ k}\Omega} = 3.0\text{ mA}$$

---

##### 4. Evaluar (Comprobación física y coherencia de balance)
1. **Comprobación de Corrientes de Todas las Ramas:**
   * $I_1 = \dfrac{V_A - V_{N1}}{R_1} = \dfrac{12\text{ V} - 6\text{ V}}{2\text{ k}\Omega} = 3.0\text{ mA}$ (fluye de $V_A$ hacia $N_1$, signo positivo confirma sentido asumido).
   * $I_2 = \dfrac{V_{N1}}{R_2} = \dfrac{6\text{ V}}{4\text{ k}\Omega} = 1.5\text{ mA}$ (fluye de $N_1$ a $\text{GND}$, signo positivo confirma sentido asumido).
   * $I_3 = 3.0\text{ mA}$ (como $V_{N1} = 6\text{ V} > V_B = 3\text{ V}$, el flujo real es efectivamente desde $N_1$ hacia $V_B$).
   * $I_s = 1.5\text{ mA}$ (inyectada hacia $N_1$).

2. **Balance de LCK en el Nodo $N_1$:**
   $$\sum I_{\text{entrantes}} = I_1 + I_s = 3.0\text{ mA} + 1.5\text{ mA} = 4.5\text{ mA}$$
   $$\sum I_{\text{salientes}} = I_2 + I_3 = 1.5\text{ mA} + 3.0\text{ mA} = 4.5\text{ mA}$$
   $$4.5\text{ mA} \equiv 4.5\text{ mA} \quad \checkmark \ (\text{Balance exacto comprobado})$$

3. **Conclusión de Ingeniería:**
   El potencial en el punto de interconexión es $V_{N1} = 6.0\text{ V}$. La corriente por $R_3$ tiene una magnitud de $3.0\text{ mA}$ y viaja saliendo del nodo $N_1$ en dirección hacia la fuente $V_B$. Potencia disipada en $R_3$: $P_{R3} = I_3^2 \cdot R_3 = (3\text{ mA})^2 \cdot 1\text{ k}\Omega = 9\text{ mW}$, perfectamente compatible con resistencias estándar de $1/8\text{ W}$ o $1/16\text{ W}$ (SMD 0603/0805).

---

### 3. 📚 Ficha de Repaso Cornell-Kwik (Para Dominio Rápido)

#### 📋 Ficha Técnica (Estilo Cornell)

| Claves / Preguntas Clave | Detalles Técnicos (Respuestas Directas) |
| --- | --- |
| **Concepto / Ley Principal** | Principio de conservación de la carga: La suma de corrientes en un nodo es cero. |
| **Ecuación Fundamental** | `Σ I_entrantes = Σ I_salientes` |
| **Error Común a Evitar** | Errores en la asignación de signos algebraicos al expresar diferencias de potencial ($V_{\text{inicio}} - V_{\text{fin}}$) para las corrientes. |
| **Relación con Electrónica I y II** | Ecuación fundamental en transistores $I_E = I_B + I_C$ y en la regla de masa virtual para amplificadores operacionales. |

#### 💡 Análisis Creativo (Estilo Kwik)

* **Analogía (Create):** Un nodo es como una rotonda o cruce de tráfico: la cantidad de automóviles que ingresan a la rotonda por minuto debe ser exactamente igual a la cantidad de automóviles que salen de ella para que no se produzcan embotellamientos ni se generen autos mágicamente.
* **Duda Crítica (Inquire):** *¿Qué sucede con la LCK si conectamos una fuente ideal de voltaje directamente entre dos nodos sin resistencia serie?* Se forma un **Supernodo**, requiriendo una ecuación combinada de nodos junto con la restricción de diferencia de potencial de la fuente.
* **Prueba de Fuego (Apply):** Si a un nodo ingresan dos corrientes de $4\text{ mA}$ y $2.5\text{ mA}$, y sale una rama de $1\text{ mA}$, ¿cuánta corriente fluye por la última rama saliente? ($I_{\text{restante}} = 4 + 2.5 - 1 = 5.5\text{ mA}$).

---

### 4. 🛠️ Herramientas Digitales y Simulación

* **Prompt para Mini App Interactiva (Gemini Canvas / HTML5):**
> *"Genera una aplicación web interactiva en un solo archivo HTML/JS autocontenido que modele la Ley de Corrientes de Kirchhoff (LCK) en un nodo principal conectado a 4 ramas (2 de entrada con corrientes ajustables de 0 a 10 mA, y 2 de salida). Incluye controles deslizantes para modificar las corrientes entrantes $I_1$ e $I_2$, y el valor de una resistencia de salida $R_1$. La app debe calcular de forma dinámica la corriente restante $I_4$, mostrar un diagrama vectorial/animado del nodo indicando el sentido de los electrones y advertir visualmente la conservación de carga."*



