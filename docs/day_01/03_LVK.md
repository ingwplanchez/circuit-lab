# 📌 Día 1 - Lección 3: Ley de Tensiones de Kirchhoff (LVK) y Conservación de la Energía

**Objetivo de Ingeniería / Electrónica:** Dominar el análisis de elevaciones y caídas de potencial a lo largo de mallas cerradas para determinar voltajes de nodo, caídas de tensión en componentes y la potencia intercambiada en circuitos de CD y etapas de polarización.

**Agenda de Tiempo:**

* **Bloque de estudio enfocado (45 min):** Definición de malla y lazo cerrado, principio de conservación de la energía, convención de signos pasiva y resolución de circuitos de múltiples mallas.

---

### 1. 🖊️ Guión Rápido de Repaso (Diseñado para dominio conceptual veloz)

* **Fundamentos Teóricos & Conexión Electrónica:**
* La **Ley de Tensiones de Kirchhoff (LVK)** se deriva directamente del principio físico de **conservación de la energía**: el trabajo neto realizado al mover una carga a lo largo de una trayectoria cerrada o malla en un campo eléctrico es igual a cero.
* Una **malla** es una trayectoria cerrada que no contiene ninguna otra trayectoria cerrada en su interior. La suma algebraica de todas las tensiones (elevaciones y caídas) alrededor de cualquier malla cerrada debe ser estrictamente cero.
* **Conexión con Electrónica I y II:** La LVK es la base para analizar la **Línea de Carga de CD y CA** en transistores BJT y MOSFET, así asumiendo las mallas de entrada (base-emisor o compuerta-fuente) y de salida (colector-emisor o drenador-fuente). También es indispensable para el cálculo de respuesta en frecuencia e impedancias mediante mallas de señal pequeña.


* **Las 3 Fórmulas Esenciales:**
1. **LVK en Forma General (Sumatoria Algebraica):**

$$\sum_{k=1}^{N} V_k = 0 \quad \text{(alrededor de cualquier lazo cerrado)}$$


2. **LVK en Forma Elevaciones vs Caídas:**

$$\sum V_{\text{elevaciones}} = \sum V_{\text{caídas}}$$


3. **Convención de Signos Pasiva (Tensión en Resistencia):**

$$V_R = I \cdot R \quad \text{(la corriente entra por el terminal positivo } + \text{ y sale por el } -\text{)}$$




* **Diagrama de Análisis (Esquema Visual de una Malla Cerrada):**

```text
          ───[ R1 ]───► (I_malla)
        ┌──────────────┐
        │              │
       (Vs)           [ R2 ]
        │              │
        └──────────────┘
          ───[ R3 ]───◄

   Ecuación LVK: Vs - I*R1 - I*R2 - I*R3 = 0

```

* **Estrategia IPEE de Resolución de Problemas (Paso a Paso):**
1. *Identificar:* Definir los lazos o mallas independientes del circuito y asignar un sentido arbitrario de circulación de corriente de malla (habitualmente en sentido horario).
2. *Plantear:* Recorrer la malla en la dirección elegida anotando el signo del primer terminal que se encuentre en cada componente (elevación: $-$ a $+$ $\rightarrow$ $+V$; caída: $+$ a $-$ $\rightarrow$ $-V$).
3. *Ejecutar:* Escribir la ecuación sumatoria para cada malla sustituyendo las caídas de tensión en resistencias mediante la Ley de Ohm ($V_R = I \cdot R$).
4. *Evaluar:* Resolver el sistema de ecuaciones algebraicas y verificar los voltajes absolutos mediante simuladores o comprobación de potencia total sumada.



---

### 2. 📐 Ejercicio Resuelto Paso a Paso (Enfoque Práctico)

* **Contexto de Electrónica:** Análisis de la malla de polarización de entrada/salida para un circuito de etapa discreta con dos fuentes de alimentación.
* **Enunciado del Problema:**
Considere un circuito compuesto por una malla única cerrada con los siguientes elementos conectados en serie:
* Una fuente principal de voltaje $V_{S1} = 24\text{ V}$.
* Una resistencia $R_1 = 1.2\text{ k}\Omega$.
* Una resistencia $R_2 = 2.2\text{ k}\Omega$.
* Una segunda fuente de voltaje opuesta $V_{S2} = 6\text{ V}$.
* Una resistencia $R_3 = 680\ \Omega$.


*Calcule la corriente de malla $I$, la caída de voltaje en cada resistencia y demuestre el cumplimiento de la LVK recorriendo la malla.*

* **Diagrama Esquemático del Circuito:**

```text
                  +   VR1  -             +   VR2  -
         ┌─────[ R1 = 1.2 kΩ ]─────────[ R2 = 2.2 kΩ ]─────┐
         │                                                 │
       + │                                               + │
    ( VS1 = 24 V )          I (Horario)               ( VS2 = 6 V )
       - │                      ↻                        - │
         │                                                 │
         └─────────────────[ R3 = 680 Ω ]──────────────────┘
                            -   VR3  +
```

* **Desarrollo Numérico Completo:**
1. *Paso 1 (Asignar dirección de corriente y polaridad en elementos pasivos):*
* Asumimos una corriente $I$ circulando en sentido horario.
* La corriente entra por el polo positivo de los resistores, polarizándolos: $R_1 (+,-)$, $R_2 (+,-)$, $R_3 (+,-)$.
* La fuente $V_{S1}$ se recorre de $-$ a $+$ (elevación). La fuente $V_{S2}$ se encuentra polarizada en oposición y se recorre de $+$ a $-$ (caída).


2. *Paso 2 (Plantear la ecuación de la LVK):*

$$\sum V = 0$$


$$+V_{S1} - V_{R1} - V_{R2} - V_{S2} - V_{R3} = 0$$


$$24 - (I \cdot R_1) - (I \cdot R_2) - 6 - (I \cdot R_3) = 0$$


3. *Paso 3 (Ejecutar el despeje de la corriente $I$):*
Sustituyendo valores de resistencia ($1.2\text{ k}\Omega + 2.2\text{ k}\Omega + 0.68\text{ k}\Omega = 4.08\text{ k}\Omega$):

$$24 - 6 = I \cdot (R_1 + R_2 + R_3)$$


$$18\text{ V} = I \cdot (4080\ \Omega)$$


$$I = \frac{18\text{ V}}{4080\ \Omega} \approx 4.412\text{ mA}$$


4. *Paso 4 (Evaluar las caídas de tensión individuales y verificar la LVK):*
* $V_{R1} = I \cdot R_1 = 4.412\text{ mA} \times 1.2\text{ k}\Omega = 5.294\text{ V}$
* $V_{R2} = I \cdot R_2 = 4.412\text{ mA} \times 2.2\text{ k}\Omega = 9.706\text{ V}$
* $V_{R3} = I \cdot R_3 = 4.412\text{ mA} \times 0.68\text{ k}\Omega = 3.000\text{ V}$


*Comprobación de LVK:*

$$\sum V = +24\text{ V} - 5.294\text{ V} - 9.706\text{ V} - 6\text{ V} - 3.000\text{ V} = 24 - 24 = 0\text{ V} \quad \checkmark$$





---

### 3. 📚 Ficha de Repaso Cornell-Kwik (Para Dominio Rápido)

#### 📋 Ficha Técnica (Estilo Cornell)

| Claves / Preguntas Clave | Detalles Técnicos (Respuestas Directas) |
| --- | --- |
| **Concepto / Ley Principal** | Principio de conservación de la energía: La suma algebraica de voltajes en un lazo cerrado es cero. |
| **Ecuación Fundamental** | `Σ V_elevaciones = Σ V_caídas` |
| **Error Común a Evitar** | Confundir el sentido de recorrido de la malla con la dirección real de la corriente o no respetar el signo del terminal de entrada. |
| **Relación con Electrónica I y II** | Ecuación de la Malla de Salida en BJT: $V_{CC} - I_C R_C - V_{CE} - I_E R_E = 0$. |

#### 💡 Análisis Creativo (Estilo Kwik)

* **Analogía (Create):** Una malla eléctrica es como una montaña rusa cerrada: las fuentes representan los motores que suben el vagón a cierta altura (elevación de potencial), mientras que las resistencias son las descensos o tramos donde se pierde la altura ganada (caídas de potencial), volviendo exactamente al nivel inicial al finalizar la vuelta.
* **Duda Crítica (Inquire):** *¿Qué ocurre con la LVK si una malla contiene una fuente ideal de corriente compartida entre dos lazos?* Se genera una **Supermalla**, la cual requiere excluir temporalmente la fuente de corriente para escribir la LVK en el lazo perimétrico exterior.
* **Prueba de Fuego (Apply):** Si en una malla con una fuente de $15\text{ V}$ hay dos resistencias cuyas caídas medidas son $4.5\text{ V}$ y $3.5\text{ V}$, ¿cuál es la caída de voltaje en el tercer componente de la malla? ($V_3 = 15 - 4.5 - 3.5 = 7.0\text{ V}$).

---

### 4. 🛠️ Herramientas Digitales y Simulación

* **Prompt para Mini App Interactiva (Gemini Canvas / HTML5):**
> *"Genera una aplicación web interactiva en un solo archivo HTML/JS autocontenido que modele la Ley de Tensiones de Kirchhoff (LVK) en una malla de 3 componentes (una fuente de voltaje ajustable de 5V a 24V y dos resistencias R1 y R2). La interfaz debe incluir controles deslizantes para ajustar los valores, mostrar un gráfico circular o barra de elevación vs caídas de tensión en tiempo real y desplegar la ecuación dinámica sumatoria demostrando que la suma de voltajes es exactamente igual a cero."*


