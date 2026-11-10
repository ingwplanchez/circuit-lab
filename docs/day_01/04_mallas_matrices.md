# 📌 Día 1 - Lección 4: Método de Corrientes de Malla (Aplicación Sistemática)

**Objetivo de Ingeniería / Electrónica:** Dominar el planteamiento sistemático y matricial de ecuaciones de malla para resolver circuitos de múltiples lazos, habilidad crítica para calcular las mallas de entrada y salida simultáneas en circuitos transistorizados complejos con realimentación.

**Agenda de Tiempo:**

* **Bloque de estudio enfocado (45 min):** Definición de mallas independientes, corrientes ficticias de malla, inspección de resistencias propias y mutuas, y tratamiento de fuentes de corriente independientes (supermallas).

---

### 1. 🖊️ Guión Rápido de Repaso (Diseñado para dominio conceptual veloz)

* **Fundamentos Teóricos & Conexión Electrónica:**
* El **Método de Corrientes de Malla** sistematiza la aplicación de la Ley de Tensiones de Kirchhoff (LVK) asignando corrientes ficticias (corrientes de malla) a cada ventana o lazo cerrado independiente del circuito.
* En lugar de escribir la LVK de forma manual y desordenada para cada componente, el método de mallas permite construir directamente un sistema de ecuaciones lineales ordenado, a menudo expresado en forma matricial $[R][I] = [V]$.
* **Conexión con Electrónica I y II:** Es la herramienta clave para resolver circuitos polarizados con múltiples fuentes de alimentación (por ejemplo, alimentación dual $\pm V_{CC}$ y $-V_{EE}$ en amplificadores operacionales o etapas diferenciales de transistores), donde convergen varias mallas interconectadas.


* **Las 3 Fórmulas Esenciales:**
1. **Ecuación General de Malla (por inspección):**

$$\sum (\text{Resistencias Propias y Mutuas}) \cdot I_{\text{malla}} = \sum \text{Voltajes de la Malla}$$


2. **Forma Matricial Estándar:**

$$\begin{bmatrix} R_{11} & -R_{12} \\ -R_{21} & R_{22} \end{bmatrix} \begin{bmatrix} I_1 \\ I_2 \end{bmatrix} = \begin{bmatrix} V_s1 \\ V_s2 \end{bmatrix}$$


3. **Caída de Corriente en una Rama Compartida:**

$$I_{\text{rama}} = I_{\text{malla A}} - I_{\text{malla B}} \quad \text{(según la orientación de la rama)}$$




* **Diagrama de Análisis (Esquema Visual de una Red de Dos Mallas):**

```text
          (Malla 1: I1)           (Malla 2: I2)
        ┌──────[ R1 ]──────┐──────[ R2 ]──────┐
        │                  │                  │
       (Vs1)             [ R3 ]             (Vs2)
        │                  │                  │
        └──────────────────┴──────────────────┘

```

* **Estrategia IPEE de Resolución de Problemas (Paso a Paso):**
1. *Identificar:* Contar el número de ventanas o mallas independientes ($M = B - N + 1$). Asignar a cada malla una corriente ficticia circulando en sentido horario ($I_1, I_2, \dots$).
2. *Plantear:* Para cada malla, sumar todas las resistencias contenidas en su perímetro multiplicadas por su propia corriente de malla, y restar las resistencias compartidas multiplicadas por las corrientes de las mallas vecinas. Igualar a la suma algebraica de fuentes de voltaje en esa malla.
3. *Ejecutar:* Resolver el sistema de ecuaciones simultáneas (por sustitución, regla de Cramer o inversión de matrices).
4. *Evaluar:* Obtener las corrientes reales de rama restando o sumando las corrientes de malla correspondientes, y comprobar la disipación de potencia total.



---

### 2. 📐 Ejercicio Resuelto Paso a Paso (Enfoque Práctico)

* **Contexto de Electrónica:** Análisis de una red de polarización resistiva de dos mallas alimentada por una fuente de voltaje continua, simulando una etapa de divisor con carga acoplada.
* **Enunciado del Problema:**
Dado un circuito de dos mallas coplanares:
* Malla 1: Contiene una fuente de voltaje $V_s = 12\text{ V}$, una resistencia $R_1 = 2\text{ k}\Omega$ y una resistencia central compartida $R_3 = 4\text{ k}\Omega$.
* Malla 2: Contiene la resistencia central compartida $R_3 = 4\text{ k}\Omega$ y una resistencia de carga $R_2 = 2\text{ k}\Omega$.
* *Calcule las corrientes de malla $I_1$ e $I_2$ y la corriente real que fluye a través de la resistencia central $R_3$.*

* **Diagrama Esquemático del Circuito:**

```text
                     ( Malla 1 )                          ( Malla 2 )
         ┌──────[ R1 = 2 kΩ ]──────┬───────────────────────────────────┐
         │                         │                                   │
       + │                         │                                   │
  ( Vs = 12 V )      I1            │ IR3 = I1 - I2               [ R2 = 2 kΩ ]
       - │            ↻            │        ▼                          │
         │                   [ R3 = 4 kΩ ]              I2             │
         │                         │                     ↻             │
         │                         │                                   │
         └─────────────────────────┴───────────────────────────────────┘
```

* **Desarrollo Numérico Completo:**
1. *Paso 1 (Definir mallas y resistencias propias/mutuas):*
* Malla 1 (Resistencias propias): $R_{11} = R_1 + R_3 = 2\text{ k}\Omega + 4\text{ k}\Omega = 6\text{ k}\Omega$.
* Malla 2 (Resistencias propias): $R_{22} = R_2 + R_3 = 2\text{ k}\Omega + 4\text{ k}\Omega = 6\text{ k}\Omega$.
* Resistencia mutua compartida: $R_{12} = R_{21} = R_3 = 4\text{ k}\Omega$.


2. *Paso 2 (Plantear el sistema de ecuaciones de malla):*
* Para Malla 1:

$$R_{11}I_1 - R_{12}I_2 = V_{s1} \implies 6I_1 - 4I_2 = 12$$


* Para Malla 2 (sin fuente propia de voltaje):

$$R_{22}I_2 - R_{21}I_1 = 0 \implies 6I_2 - 4I_1 = 0 \implies I_1 = 1.5 I_2$$




3. *Paso 3 (Ejecutar la solución del sistema algebraico):*
Sustituyendo $I_1 = 1.5 I_2$ en la ecuación de la Malla 1:

$$6(1.5 I_2) - 4I_2 = 12$$


$$9I_2 - 4I_2 = 12 \implies 5I_2 = 12 \implies I_2 = \frac{12}{5} = 2.4\text{ mA}$$



Calculando $I_1$:

$$I_1 = 1.5 \times 2.4\text{ mA} = 3.6\text{ mA}$$


4. *Paso 4 (Evaluar la corriente real en la resistencia central $R_3$):*
Asumiendo que $R_3$ es compartida por ambas mallas en sentidos opuestos:

$$I_{R3} = I_1 - I_2 = 3.6\text{ mA} - 2.4\text{ mA} = 1.2\text{ mA}$$



*(El resultado muestra una corriente neta de $1.2\text{ mA}$ fluyendo hacia abajo por $R_3$, coherente con la polaridad de la fuente principal).*



---

### 3. 📚 Ficha de Repaso Cornell-Kwik (Para Dominio Rápido)

#### 📋 Ficha Técnica (Estilo Cornell)

| Claves / Preguntas Clave | Detalles Técnicos (Respuestas Directas) |
| --- | --- |
| **Concepto / Ley Principal** | Aplicación sistemática de la LVK mediante corrientes ficticias de lazo o malla. |
| **Ecuación Fundamental** | `[R_propia] * I_malla - [R_mutua] * I_vecina = Σ V_fuentes` |
| **Error Común a Evitar** | Olvidar restar la resistencia mutua en las ecuaciones de malla adyacentes o ignorar el sentido de las fuentes. |
| **Relación con Electrónica I y II** | Solución de redes de polarización con múltiples fuentes y circuitos amplificadores multietapa. |

#### 💡 Análisis Creativo (Estilo Kwik)

* **Analogía (Create):** Las corrientes de malla son como dos corredores que dan vueltas en pistas circulares adyacentes que comparten un carril central; en ese carril compartido, la velocidad neta y el esfuerzo dependen de la diferencia de velocidad entre ambos corredores.
* **Duda Crítica (Inquire):* *¿Qué pasa si una fuente de corriente independiente se encuentra exactamente en la frontera entre dos mallas?* Se genera una **Supermalla**, lo que obliga a eliminar temporalmente la fuente abriendo la rama y combinando ambas mallas en una sola trayectoria perimétrica.
* **Prueba de Fuego (Apply):** Si en un sistema de dos mallas las ecuaciones resultantes son $5I_1 - 2I_2 = 10$ y $-2I_1 + 4I_2 = 0$, ¿cuánto vale $I_2$? ($I_2 = 0.5 I_1$; sustituyendo: $5I_1 - 2(0.5 I_1) = 10 \implies 4I_1 = 10 \implies I_1 = 2.5\text{ mA}$, por lo que $I_2 = 1.25\text{ mA}$).

---

### 4. 🛠️ Herramientas Digitales y Simulación

* **Prompt para Mini App Interactiva (Gemini Canvas / HTML5):**
> *"Genera una aplicación web interactiva en un solo archivo HTML/JS autocontenido que modele el Método de Corrientes de Malla en un circuito de dos lazos con una fuente de voltaje ajustable $V_s$ ($5\text{V}$ a $20\text{V}$) y tres resistencias ($R_1, R_2, R_3$). La interfaz debe incluir controles deslizantes para modificar los valores de las resistencias, calcular de forma dinámica las corrientes de malla $I_1$ e $I_2$ mediante determinantes matriciales, y mostrar un diagrama visual con flechas animadas indicando la dirección y magnitud del flujo de corriente en la resistencia central compartida."*

---

## Multiplicación de matrices

La matriz de corrientes $\begin{bmatrix} I_1 \\ I_2 \end{bmatrix}$ tiene 2 filas y 1 columna, por lo que es una matriz de **$2 \times 1$** (un *vector columna*). Una matriz de $1 \times 2$ estaría acostada (una fila y dos columnas).

Para que la multiplicación de matrices sea válida, la regla de oro es que **el número de columnas de la primera matriz debe ser igual al número de filas de la segunda**:


$$(2 \times \mathbf{2}) \times (\mathbf{2} \times 1) = (2 \times 1)$$


¡Los números del centro coinciden ($2$ y $2$), por lo que la multiplicación se puede hacer perfectamente y el resultado será una columna de $2 \times 1$ (exactamente igual a los voltajes)!

---

### ¿Cómo se efectúa paso a paso el producto de "Fila por Columna"?

La regla visual es: **tomas cada fila de la primera matriz y la "doblas" multiplicándola elemento por elemento contra la columna única de la segunda matriz, sumando los productos.**

Vamos a hacerlo fila por fila:

#### 1. Primera Fila de la matriz $R$ contra el vector columna $I$:

Cogemos la **Fila 1** ($\begin{bmatrix} R_{11} & -R_{12} \end{bmatrix}$) y la multiplicamos por la columna $\begin{bmatrix} I_1 \\ I_2 \end{bmatrix}$:

* Multiplicas el primer elemento con el primer elemento: $R_{11} \cdot I_1$
* Multiplicas el segundo elemento con el segundo elemento: $-R_{12} \cdot I_2$
* Los sumas:

$$(R_{11} \cdot I_1) + (-R_{12} \cdot I_2)$$



Esto se iguala al primer elemento de la matriz resultado ($V_{s1}$):


$$(R_{11} \cdot I_1) - (R_{12} \cdot I_2) = V_{s1} \quad \text{--- (¡Esta es la ecuación de la Malla 1!)}$$

---

#### 2. Segunda Fila de la matriz $R$ contra el vector columna $I$:

Cogemos la **Fila 2** ($\begin{bmatrix} -R_{21} & R_{22} \end{bmatrix}$) y hacemos exactamente lo mismo con la misma columna $\begin{bmatrix} I_1 \\ I_2 \end{bmatrix}$:

* Multiplicas el primer elemento con el primero: $-R_{21} \cdot I_1$
* Multiplicas el segundo elemento con el segundo: $R_{22} \cdot I_2$
* Los sumas:

$$(-R_{21} \cdot I_1) + (R_{22} \cdot I_2)$$



Esto se iguala al segundo elemento de la matriz resultado ($V_{s2}$):


$$(-R_{21} \cdot I_1) + (R_{22} \cdot I_2) = V_{s2} \quad \text{--- (¡Esta es la ecuación de la Malla 2!)}$$

---

### En Resumen:

La multiplicación matricial es solo un empaque matemático compacto. En lugar de escribir las dos ecuaciones largas de la LVK por separado:

1. $(R_{11} \cdot I_1) - (R_{12} \cdot I_2) = V_{s1}$
2. $(-R_{21} \cdot I_1) + (R_{22} \cdot I_2) = V_{s2}$

Los ingenieros agrupamos las resistencias en una caja ($2 \times 2$), las corrientes en una columna ($2 \times 1$) y las fuentes en otra columna ($2 \times 1$) para que la computadora o el análisis matricial procese el sistema de forma limpia.
---

## ✏️ Regla de Cramer para circuitos de dos mallas

El siguiente texto es un fragmento de un libro de texto de circuitos que explica paso a paso cómo resolver matrices de dos mallas utilizando la Regla de Cramer, que es un método algebraico muy útil para sistemas de ecuaciones lineales. Este texto está diseñado para ser fácil de entender y aplicar en el contexto de la resolución de circuitos eléctricos.

Vamos a desglosarlo **paso a paso** desde cero.

---

### Paso 1: Traducir la matriz a un sistema de ecuaciones normal

Una multiplicación de matrices no es más que una forma elegante y compacta de escribir un sistema de ecuaciones simultáneas. Si multiplicas filas por columnas en tu expresión:

$$\begin{bmatrix} R_{11} & -R_{12} \\ -R_{21} & R_{22} \end{bmatrix} \begin{bmatrix} I_1 \\ I_2 \end{bmatrix} = \begin{bmatrix} V_{s1} \\ V_{s2} \end{bmatrix}$$

Obtienes exactamente dos ecuaciones algebraicas con dos incógnitas ($I_1$ e $I_2$):

1. **Ecuación de la Malla 1:** $(R_{11} \cdot I_1) - (R_{12} \cdot I_2) = V_{s1}$
2. **Ecuación de la Malla 2:** $(-R_{21} \cdot I_1) + (R_{22} \cdot I_2) = V_{s2}$

---

### Paso 2: Aplicar la Regla de Cramer (El método del determinante)

La Regla de Cramer utiliza **determinantes** (simbolizados con un triángulo $\Delta$). Para resolver el sistema, solo necesitamos calcular tres determinantes:

1. El **determinante del sistema ($\Delta$)**: Se forma únicamente con los coeficientes de las resistencias.
2. El **determinante para la corriente 1 ($\Delta_1$)**: Sustituye la primera columna de resistencias por los voltajes de las fuentes.
3. El **determinante para la corriente 2 ($\Delta_2$)**: Sustituye la segunda columna de resistencias por los voltajes de las fuentes.

Las fórmulas finales siempre serán:


$$I_1 = \frac{\Delta_1}{\Delta} \quad \text{y} \quad I_2 = \frac{\Delta_2}{\Delta}$$

---

### Paso 3: Ejemplo Numérico Real (Usando los datos del ejercicio anterior)

Supongamos los valores numéricos que tuvimos en la lección:

* Resistencias propias: $R_{11} = 6\text{ k}\Omega$, $R_{22} = 6\text{ k}\Omega$
* Resistencia mutua (compartida): $R_{12} = R_{21} = 4\text{ k}\Omega$
* Fuentes de voltaje: $V_{s1} = 12\text{ V}$, $V_{s2} = 0\text{ V}$

La matriz numérica queda así:


$$\begin{bmatrix} 6 & -4 \\ -4 & 6 \end{bmatrix} \begin{bmatrix} I_1 \\ I_2 \end{bmatrix} = \begin{bmatrix} 12 \\ 0 \end{bmatrix}$$

#### 1. Calcular el determinante principal del sistema ($\Delta$):

Para calcular el determinante de una matriz de $2 \times 2$, multiplicas la diagonal principal y le restas la multiplicación de la diagonal secundaria: $\Delta = (a \cdot d) - (b \cdot c)$.


$$\Delta = \begin{vmatrix} 6 & -4 \\ -4 & 6 \end{vmatrix} = (6 \cdot 6) - (-4 \cdot -4)$$

$$\Delta = 36 - (16) = 20$$

#### 2. Calcular el determinante de la Corriente 1 ($\Delta_1$):

Sustituimos la **primera columna** de la matriz de resistencias $\begin{bmatrix} 6 \\ -4 \end{bmatrix}$ por la columna de fuentes $\begin{bmatrix} 12 \\ 0 \end{bmatrix}$:


$$\Delta_1 = \begin{vmatrix} 12 & -4 \\ 0 & 6 \end{vmatrix} = (12 \cdot 6) - (-4 \cdot 0)$$

$$\Delta_1 = 72 - 0 = 72$$

#### 3. Calcular el determinante de la Corriente 2 ($\Delta_2$):

Sustituimos la **segunda columna** de la matriz de resistencias $\begin{bmatrix} -4 \\ 6 \end{bmatrix}$ por la columna de fuentes $\begin{bmatrix} 12 \\ 0 \end{bmatrix}$:


$$\Delta_2 = \begin{vmatrix} 6 & 12 \\ -4 & 0 \end{vmatrix} = (6 \cdot 0) - (12 \cdot -4)$$

$$\Delta_2 = 0 - (-48) = 48$$

---

### Paso 4: Obtener los valores finales de Corriente

Ahora solo dividimos cada determinante entre el determinante principal $\Delta$:

* **Corriente de Malla 1 ($I_1$):**

$$I_1 = \frac{\Delta_1}{\Delta} = \frac{72}{20} = 3.6\text{ mA}$$


* **Corriente de Malla 2 ($I_2$):**

$$I_2 = \frac{\Delta_2}{\Delta} = \frac{48}{20} = 2.4\text{ mA}$$


---

### La Regla de Oro para el Determinante de $2 \times 2$ (El Método del Aspa o Cruz)

Imagina que tienes una caja con 4 números dispuesta en un determinante de $2 \times 2$:


$$\begin{vmatrix} \text{Elemento A} & \text{Elemento B} \\ \text{Elemento C} & \text{Elemento D} \end{vmatrix}$$

Para calcular el determinante de esta caja, la regla matemática fija una operación en forma de **X** (o aspa):

1. **La Diagonal Principal (de arriba-izquierda hacia abajo-derecha):** Multiplicas esos dos números y el resultado conserva su **signo positivo**.

$$\text{Multiplicación 1} = (\text{Elemento A} \cdot \text{Elemento D})$$


2. **La Diagonal Secundaria (de arriba-derecha hacia abajo-izquierda):** Multiplicas esos dos números y al resultado **obligatoriamente se le cambia el signo** (o se le resta a la multiplicación anterior).

$$\text{Multiplicación 2} = (\text{Elemento B} \cdot \text{Elemento C})$$



La fórmula universal de cualquier determinante de $2 \times 2$ es siempre la misma:


$$\text{Determinante} = (\text{A} \cdot \text{D}) - (\text{B} \cdot \text{C})$$

---

### Vamos a aplicarlo paso a paso a nuestros tres determinantes del circuito

Recuerda que nuestra matriz original de resistencias y fuentes era:


$$\begin{bmatrix} 6 & -4 \\ -4 & 6 \end{bmatrix} \begin{bmatrix} I_1 \\ I_2 \end{bmatrix} = \begin{bmatrix} 12 \\ 0 \end{bmatrix}$$

---

#### 1. Calculando el Determinante del Sistema ($\Delta$)

Usamos únicamente la matriz de las resistencias:


$$\Delta = \begin{vmatrix} 6 & -4 \\ -4 & 6 \end{vmatrix}$$


Identificamos quién es quién en el esquema de la **X**:

* **A** = $6$ (esquina superior izquierda)
* **B** = $-4$ (esquina superior derecha)
* **C** = $-4$ (esquina inferior izquierda)
* **D** = $6$ (esquina inferior derecha)

Hacemos las multiplicaciones en cruz:

* **Diagonal Principal ($A \cdot D$):** $(6) \cdot (6) = \mathbf{36}$
* **Diagonal Secundaria ($B \cdot C$):** $(-4) \cdot (-4) = \mathbf{16}$ *(positivo porque menos por menos es más)*

Juntamos ambos resultados restándolos (como manda la fórmula):


$$\Delta = (36) - (16) = \mathbf{20}$$


*(De ahí sale el $20$ del denominador).*

---

#### 2. Calculando el Determinante de la Corriente 1 ($\Delta_1$)

Aquí viene el "truco" de Cramer para despejar $I_1$: **agarras la columna de las fuentes** $\begin{bmatrix} 12 \\ 0 \end{bmatrix}$ y **reemplazas con ella la primera columna** de la matriz de resistencias.

La matriz de resistencias era $\begin{bmatrix} \mathbf{6} & -4 \\ \mathbf{-4} & 6 \end{bmatrix}$. Quitamos la columna en negrita y ponemos las fuentes:


$$\Delta_1 = \begin{vmatrix} \mathbf{12} & -4 \\ \mathbf{0} & 6 \end{vmatrix}$$

Volvemos a aplicar la misma regla de la **X** con estos nuevos números:

* **A** = $12$, **B** = $-4$, **C** = $0$, **D** = $6$
* **Diagonal Principal ($A \cdot D$):** $(12) \cdot (6) = \mathbf{72}$
* **Diagonal Secundaria ($B \cdot C$):** $(-4) \cdot (0) = \mathbf{0}$

Restamos ambos resultados:


$$\Delta_1 = (72) - (0) = \mathbf{72}$$


*(De ahí sale el $72$ que luego dividiremos entre 20 para hallar $I_1$).*

---

#### 3. Calculando el Determinante de la Corriente 2 ($\Delta_2$)

Para hallar $I_2$, hacemos lo mismo pero **reemplazando la segunda columna** de la matriz de resistencias por la columna de fuentes $\begin{bmatrix} 12 \\ 0 \end{bmatrix}$.

La matriz original era $\begin{bmatrix} 6 & \mathbf{-4} \\ -4 & \mathbf{6} \end{bmatrix}$. Quitamos la columna de la derecha y ponemos las fuentes:


$$\Delta_2 = \begin{vmatrix} 6 & \mathbf{12} \\ -4 & \mathbf{0} \end{vmatrix}$$

Aplicamos por última vez la regla de la **X**:

* **A** = $6$, **B** = $12$, **C** = $-4$, **D** = $0$
* **Diagonal Principal ($A \cdot D$):** $(6) \cdot (0) = \mathbf{0}$
* **Diagonal Secundaria ($B \cdot C$):** $(12) \cdot (-4) = \mathbf{-48}$

Restamos ambos resultados (cuidado con el doble signo de la resta y el menos del 48):


$$\Delta_2 = (0) - (-48) = 0 + 48 = \mathbf{48}$$


*(De ahí sale el $48$ que al dividirlo entre 20 nos da los $2.4\text{ mA}$ de $I_2$).*

---

### Resumen visual de la "Cruz"

Cada vez que veas un determinante de $2 \times 2$, piensa siempre en esto:


$$\begin{vmatrix} \text{Arriba-Izquierda} & \text{Arriba-Derecha} \\ \text{Abajo-Izquierda} & \text{Abajo-Derecha} \end{vmatrix} = [(\text{Esq. Sup-Izq} \cdot \text{Esq. Inf-Der}) - (\text{Esq. Sup-Der} \cdot \text{Esq. Inf-Izq})]$$





