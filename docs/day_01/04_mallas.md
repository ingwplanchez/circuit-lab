# 📌 Día 1 - Lección 4 (Alternativa): Método de Corrientes de Malla (Solución Algebraica sin Matrices)

**Objetivo de Ingeniería / Electrónica:** Dominar el planteamiento y resolución de circuitos de múltiples lazos mediante corrientes de malla utilizando métodos algebraicos elementales (sustitución y reducción directa de la LVK), eliminando la necesidad de matrices, vectores o determinantes de Cramer para simplificar el cálculo mental y analítico.

**Agenda de Tiempo:**
* **Bloque de estudio enfocado (45 min):** Definición de lazos independientes, asignación de corrientes ficticias de malla, planteamiento directo de la Ley de Tensiones de Kirchhoff (LVK) y resolución del sistema de 2 ecuaciones por sustitución simple.

---

### 1. 🖊️ Guión Rápido de Repaso (Diseñado para dominio conceptual veloz)

* **Fundamentos Teóricos & Conexión Electrónica:**
  * **¿Qué es una corriente de malla?** Es una corriente imaginaria o "ficticia" ($I_1, I_2, \dots$) que suponemos da vueltas completas dentro de una ventana cerrada (malla) del circuito, casi siempre en sentido horario.
  * **La gran ventaja sin matrices:** Al usar corrientes de malla, no tenemos que inventar una variable de corriente distinta para cada resistencia. Si una resistencia está en el perímetro exterior, por ella solo pasa la corriente de esa malla. Si una resistencia está en el medio (compartida), por ella pasa la *resta* de las dos corrientes vecinas.
  * **Conexión con Electrónica I y II:** Este método se utiliza constantemente para resolver la malla de entrada (base-emisor) y la malla de salida (colector-emisor) en etapas de transistores bipolares (BJT) o MOSFET, donde una resistencia de emisor o fuente es compartida por ambos lazos.

* **Las 3 Fórmulas Esenciales (Planteamiento Directo LVK):**
  1. **LVK en Malla 1 (Recorrido Horario):**
     $$V_{\text{fuente}} - I_1 R_1 - (I_1 - I_2) R_3 = 0 \implies (R_1 + R_3)I_1 - R_3 I_2 = V_{\text{fuente}}$$
  2. **LVK en Malla 2 (Recorrido Horario):**
     $$-(I_2 - I_1) R_3 - I_2 R_2 = 0 \implies -R_3 I_1 + (R_2 + R_3)I_2 = 0$$
  3. **Corriente Real en la Rama Compartida ($R_3$):**
     $$I_{R3} = I_1 - I_2 \quad \text{(hacia abajo si } I_1 > I_2\text{)}$$

* **Diagrama de Análisis (Esquema Visual de Dos Mallas con Rama Central Compartida):**

```text
                     ( Malla 1: ↻ )                    ( Malla 2: ↻ )
         ┌──────[ R1 = 2 kΩ ]──────┬───────────────────────────────────┐
         │                         │                                   │
       + │                         │                                   │
  ( Vs = 12 V )      I1            │ IR3 = I1 - I2               [ R2 = 2 kΩ ]
       - │                         │        ▼                          │
         │                   [ R3 = 4 kΩ ]              I2             │
         │                         │                                   │
         │                         │                                   │
         └─────────────────────────┴───────────────────────────────────┘
```

* **Estrategia IPEE de Resolución de Problemas (Enfoque Algebraico Simple):**
  1. *Identificar:* Contar cuántas ventanas abiertas tiene el circuito (por ejemplo, 2 mallas). Asignar a cada una una corriente de lazo en sentido horario ($I_1$ e $I_2$).
  2. *Plantear:* Aplicar la Ley de Tensiones de Kirchhoff (LVK) recorriendo cada malla:
     * Toda resistencia por la que pasa solo una corriente causa una caída $I \cdot R$.
     * La resistencia central compartida causa una caída $(I_{\text{propia}} - I_{\text{vecina}}) \cdot R_{\text{compartida}}$.
     * Las fuentes se anotan según su signo de salida ($+$ si salimos por el positivo, $-$ si salimos por el negativo).
  3. *Ejecutar (Método de Sustitución):*
     * Despejar una variable en la ecuación más sencilla (por ejemplo, despejar $I_1$ en función de $I_2$ en la Malla 2).
     * Reemplazar esa expresión en la otra ecuación. ¡Queda una sola ecuación lineal con una sola incógnita!
     * Despejar el valor numérico y sustituir de vuelta.
  4. *Evaluar:* Calcular la corriente neta en la resistencia compartida ($I_{R3} = I_1 - I_2$) y comprobar que la potencia entregada por la fuente sea igual a la suma de potencias disipadas.

---

### 2. 📐 Ejercicio Resuelto Paso a Paso (Enfoque Práctico y 100% Algebraico)

* **Contexto de Electrónica:** Red de polarización resistiva de dos mallas que representa un divisor de tensión con una resistencia de carga acoplada ($R_2$).
* **Enunciado del Problema:**
  Dado el circuito de dos mallas:
  * **Malla 1:** Fuente de tensión continua $V_s = 12\text{ V}$, resistencia de entrada $R_1 = 2\text{ k}\Omega$ y resistencia compartida $R_3 = 4\text{ k}\Omega$.
  * **Malla 2:** Resistencia compartida $R_3 = 4\text{ k}\Omega$ y resistencia de carga $R_2 = 2\text{ k}\Omega$.
  * *Calcule las corrientes de malla $I_1$ e $I_2$, y la corriente real que circula por la resistencia central $R_3$ sin utilizar matrices.*

* **Diagrama Esquemático del Circuito:**

```text
                     ( Malla 1: ↻)                        ( Malla 2: ↻)
         ┌──────[ R1 = 2 kΩ ]──────┬───────────────────────────────────┐
         │                         │                                   │
       + │                         │                                   │
  ( Vs = 12 V )      I1            │ IR3 = I1 - I2               [ R2 = 2 kΩ ]
       - │                         │        ▼                          │
         │                   [ R3 = 4 kΩ ]              I2             │
         │                         │                                   │
         │                         │                                   │
         └─────────────────────────┴───────────────────────────────────┘
```

* **Desarrollo Numérico Completo (Paso a Paso):**

#### Paso 1: Escribir la LVK de la Malla 1
Recorremos la Malla 1 en sentido horario partiendo desde la esquina inferior izquierda:
1. Subimos por la fuente de $12\text{ V}$ (de $-$ a $+$): ganamos $+12\text{ V}$.
2. Pasamos por $R_1 = 2\text{ k}\Omega$: caída de tensión $- (I_1 \cdot 2\text{ k}\Omega)$.
3. Bajamos por la rama central $R_3 = 4\text{ k}\Omega$: por aquí baja $I_1$, pero la corriente $I_2$ de la malla vecina va subiendo en sentido contrario. Por lo tanto, la corriente neta que baja es $(I_1 - I_2)$. La caída es $- [ (I_1 - I_2) \cdot 4\text{ k}\Omega ]$.
4. Llegamos al punto de partida e igualamos a cero:

$$12 - 2 I_1 - 4(I_1 - I_2) = 0$$

Distribuyendo el producto:
$$12 - 2 I_1 - 4 I_1 + 4 I_2 = 0$$

Agrupando los términos semejantes:
$$12 - 6 I_1 + 4 I_2 = 0 \implies 6 I_1 - 4 I_2 = 12 \quad \text{--- [Ecuación 1]}$$

---

#### Paso 2: Escribir la LVK de la Malla 2
Recorremos la Malla 2 en sentido horario:
1. En la resistencia de carga $R_2 = 2\text{ k}\Omega$, solo circula $I_2$: caída $- (I_2 \cdot 2\text{ k}\Omega)$.
2. Al subir por la rama central $R_3 = 4\text{ k}\Omega$, la corriente propia $I_2$ sube, pero la corriente $I_1$ de la malla vecina baja. Por lo tanto, la corriente neta que sube es $(I_2 - I_1)$. La caída es $- [ (I_2 - I_1) \cdot 4\text{ k}\Omega ]$.
3. Como no hay fuentes en la Malla 2, igualamos a cero:

$$- 2 I_2 - 4(I_2 - I_1) = 0$$

Distribuyendo el producto:
$$- 2 I_2 - 4 I_2 + 4 I_1 = 0$$

Agrupando términos semejantes:
$$4 I_1 - 6 I_2 = 0 \quad \text{--- [Ecuación 2]}$$

---

#### Paso 3: Resolver el sistema por Sustitución Simple (¡Sin Matrices!)
Observa la **[Ecuación 2]**:
$$4 I_1 - 6 I_2 = 0$$

Pasamos el término negativo al lado derecho:
$$4 I_1 = 6 I_2$$

Despejamos $I_1$:
$$I_1 = \frac{6}{4} I_2 = 1.5 \, I_2$$

*¡Esto nos dice algo muy intuitivo: la corriente de la Malla 1 es simplemente $1.5$ veces la corriente de la Malla 2!*

Ahora sustituimos esta relación en la **[Ecuación 1]**:
$$6 I_1 - 4 I_2 = 12$$

Reemplazamos $I_1$ por $(1.5 \, I_2)$:
$$6 (1.5 \, I_2) - 4 I_2 = 12$$

Multiplicamos:
$$9 I_2 - 4 I_2 = 12$$

Restamos:
$$5 I_2 = 12$$

Despejamos $I_2$:
$$I_2 = \frac{12}{5} = \mathbf{2.4\text{ mA}}$$

---

#### Paso 4: Calcular $I_1$ y la corriente de la rama central
Como ya sabíamos que $I_1 = 1.5 \, I_2$:
$$I_1 = 1.5 \times (2.4\text{ mA}) = \mathbf{3.6\text{ mA}}$$

Finalmente, calculamos la corriente real que atraviesa la resistencia central $R_3$:
$$I_{R3} = I_1 - I_2 = 3.6\text{ mA} - 2.4\text{ mA} = \mathbf{1.2\text{ mA}}$$

*(La corriente neta en $R_3$ es de $1.2\text{ mA}$ dirigida hacia abajo).*

---

#### Paso 5: Verificación Física Inmediata (Ley de Ohm y Potencias)
Para comprobar que no hubo ningún error:
1. **Voltaje en el nodo central:**
   $$V_{\text{central}} = I_{R3} \cdot R_3 = 1.2\text{ mA} \times 4\text{ k}\Omega = 4.8\text{ V}$$
2. **Voltaje sobre $R_2$:**
   $$V_{R2} = I_2 \cdot R_2 = 2.4\text{ mA} \times 2\text{ k}\Omega = 4.8\text{ V}$$
   *¡Coincide exactamente, pues $R_3$ y $R_2$ están en paralelo con respecto a tierra!*
3. **Caída en $R_1$:**
   $$V_{R1} = I_1 \cdot R_1 = 3.6\text{ mA} \times 2\text{ k}\Omega = 7.2\text{ V}$$
4. **Suma de voltajes en la Malla 1:**
   $$V_{R1} + V_{\text{central}} = 7.2\text{ V} + 4.8\text{ V} = 12.0\text{ V} \quad \text{(¡Exactamente la fuente } V_s\text{!)}$$

Todo el circuito queda verificado sin haber escrito un solo corchete ni calculado determinantes.

---

### 3. 📚 Ficha de Repaso Cornell-Kwik (Para Dominio Rápido)

#### 📋 Ficha Técnica (Estilo Cornell)

| Claves / Preguntas Clave | Detalles Técnicos (Respuestas Directas) |
| :--- | :--- |
| **Concepto Principal** | Ley de Tensiones de Kirchhoff (LVK) expresada en función de corrientes de lazo. |
| **Ecuación en Rama Compartida** | Corriente neta $= I_{\text{malla propia}} - I_{\text{malla vecina}}$. |
| **Método de Resolución Recomendado** | **Sustitución:** Despejar una corriente de la malla pasiva (sin fuentes) y sustituirla en la malla activa. |
| **Error Típico a Evitar** | Olvidar que las dos corrientes pasan por la resistencia compartida en sentidos contrarios. |
| **Relación con Electrónica I y II** | Permite calcular con lápiz y papel el punto de operación $Q$ ($I_B, I_C, V_{CE}$) en transistores sin requerir calculadora matricial. |

#### 💡 Análisis Creativo (Estilo Kwik)

* **Analogía (Create):** Imagina dos ruedas dentadas o dos ventiladores que giran en sentido horario uno al lado del otro. En el punto de contacto central, las aspas van en direcciones contrarias: el aire neto o movimiento resultante es simplemente la diferencia de velocidades entre ambos ventiladores.
* **Duda Crítica (Inquire):** *¿Qué método algebraico es más rápido si ambas mallas tienen fuentes de alimentación?*
  El método de **Reducción / Eliminación**: se multiplica una de las ecuaciones por una constante para igualar coeficientes (por ejemplo, multiplicar por $1.5$) y se suman o restan directamente para cancelar una variable de un solo golpe.
* **Prueba de Fuego (Apply):**
  Si tienes dos ecuaciones:
  1) $5 I_1 - 2 I_2 = 10$
  2) $-2 I_1 + 4 I_2 = 0$
  ¿Cuánto vale $I_2$ por sustitución mental?
  *Respuesta:* De la (2), $4 I_2 = 2 I_1 \implies I_1 = 2 I_2$. Sustituyendo en la (1): $5(2 I_2) - 2 I_2 = 10 \implies 8 I_2 = 10 \implies I_2 = 1.25\text{ mA}$. ¡En 15 segundos sin matrices!

---

### 4. 🛠️ Herramientas Digitales y Simulación

* **Prompt para Mini App Interactiva (Gemini Canvas / HTML5):**
> *"Genera una aplicación web interactiva en un único archivo HTML/CSS/JS autocontenido que resuelva un circuito de dos mallas resistivas con una fuente de voltaje continua $V_s$ y resistencias $R_1, R_2, R_3$. La app debe permitir modificar mediante sliders o cajas de texto los valores de $V_s$, $R_1$, $R_2$ y $R_3$. En lugar de mostrar matrices, la interfaz debe mostrar un panel con el procedimiento algebraico paso a paso resuelto por el método de sustitución (mostrando las dos ecuaciones LVK simplificadas, el despeje de la variable y la sustitución numérica detallada), acompañado de un diagrama esquemático con las corrientes $I_1$, $I_2$ y la corriente resultante $I_{R3}$ calculadas en tiempo real."*
