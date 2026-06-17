**Parte A. Árboles de decisión: impureza e inducción**

**Ejercicio 1. Medidas de impureza y selección del atributo raíz**

a) Se calcularon las medidas de impureza del conjunto original obteniendo los siguientes resultados:

|     |     |
| --- | --- |
| **Medida** | **Valor** |
| Entropía inicial | 0,9852 |
| Gini inicial | 0,4898 |

b) y c) Para cada atributo se calculó la ganancia de información y la reducción de impureza medida mediante el índice de Gini:

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **Variable** | **Entropía ponderada** | **Ganancia Información** | **Gini ponderado** | **Reducción de impureza** |
| Historial | 0,7274 | 0,2578 | 0,3265 | 0,1633 |
| Deuda | 0,9740 | 0,0113 | 0,4821 | 0,0077 |
| Ingreso | 0,6046 | 0,3806 | 0,2857 | 0,2041 |

d) Ambos criterios buscan seleccionar el atributo que mejor separa las clases (Sí y No). La ganancia de información maximiza la reducción de entropía, mientras que el índice de Gini maximiza la reducción de impureza. En este conjunto de datos, el atributo Ingreso presenta los mejores valores en ambos criterios, por lo que coincide su selección como nodo raíz del árbol de decisión.

**Ejercicio 2. Inducción del árbol de decisión completo**

a) A continuación, se presenta el árbol de decisión generado a partir del conjunto de datos proporcionado.

b) A continuación se describe el árbol mediante reglas anidadas:

SI Ingreso = "Alto" ENTONCES  
Otorga = "Sí"  
<br/>SI Ingreso = "Medio" ENTONCES  
SI Historial = "Bueno" ENTONCE Otorga = "Sí"

SI Historial = "Malo" ENTONCES Otorga = "No"  
<br/>SI Ingreso = "Bajo" ENTONCES  
SI Historial = "Malo" ENTONCES Otorga = "No"  
SI Historial = "Bueno" ENTONCES

SI Deuda = "Baja" ENTONCES Otorga = "Sí"

SI Deuda = "Alta" ENTONCES Otorga = "No"

c)Las hojas son los nodos terminales donde ya se predice una clase, por lo tanto el número de hojas son 6.

Como todas las hojas son puras , es decir que quedaron separadas perfectamente, cada instancia termina en una hoja cuya clase coincide con la real. Por lo tanto, el error de resustitucion es 0

**Ejercicio 3. Partición de un atributo continuo**

a) Los puntos de corte candidatos se obtuvieron calculando el punto medio entre cada par de valores consecutivos del atributo Ingreso imponible ordenado de forma ascendente.

|     |     |
| --- | --- |
| **Intervalos** | **puntos medios** |
| 60 - 70 | 65  |
| 70 - 80 | 75  |
| 80 - 95 | 87,5 |
| 95 - 100 | 97,5 |
| 100 - 110 | 105 |
| 110 - 115 | 112,5 |
| 115 - 120 | 117,5 |
| 120 - 130 | 125 |
| 130 - 140 | 135 |

b) Para cada punto de corte candidato se calculó el índice de Gini de los subconjuntos generados y el índice de Gini ponderado de la partición binaria resultante. Los resultados obtenidos se presentan en la siguiente tabla:

|     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **Intervalos** | **puntos medios** | **Si (<= )** | **No(<= )** | **Gini (<=)** | **Si (>)** | **No(>)** | **Gini (>)** | **Gini ponderado** |
| 60 - 70 | 65  | 0   | 1   | 0   | 5   | 4   | 0,4938 | 0,4444 |
| 70 - 80 | 75  | 0   | 2   | 0   | 5   | 3   | 0,4688 | 0,3750 |
| 80 - 95 | 87,5 | 0   | 3   | 0   | 5   | 2   | 0,4082 | 0,2857 |
| 95 - 100 | 97,5 | 1   | 3   | 0,3750 | 4   | 2   | 0,4444 | 0,4167 |
| 100 - 110 | 105 | 1   | 4   | 0,3200 | 4   | 1   | 0,3200 | 0,3200 |
| 110 - 115 | 112,5 | 2   | 4   | 0,4444 | 3   | 1   | 0,3750 | 0,4167 |
| 115 - 120 | 117,5 | 3   | 4   | 0,4898 | 2   | 1   | 0,4444 | 0,4762 |
| 120 - 130 | 125 | 4   | 4   | 0,5000 | 1   | 1   | 0,5000 | 0,5000 |
| 130 - 140 | 135 | 5   | 4   | 0,4938 | 0   | 1   | 0   | 0,4444 |

c) El punto de corte óptimo es 105, ya que presenta el menor índice de Gini ponderado (0,32) entre todos los candidatos evaluados. La condición de prueba asociada al nodo es Ingreso imponible ≤ 105. Esta condición divide el conjunto de datos en dos subconjuntos: los contribuyentes con un ingreso imponible menor o igual a 105 se asignan a la rama izquierda del árbol, mientras que aquellos con un ingreso imponible superior a 105 se asignan a la rama derecha.

d) Los árboles de decisión solo generan fronteras paralelas a los ejes porque cada nodo divide los datos utilizando un único atributo a la vez. Estas particiones se realizan mediante umbrales sobre una variable, produciendo cortes alineados con los ejes del espacio de características. Por ello, las fronteras diagonales o curvas solo pueden aproximarse mediante varias divisiones consecutivas.

**Parte B. Evaluación de clasificadores**

**Ejercicio 4. Matriz de confusión y métricas de desempeño**

a) A continuación se muestra la matriz de confusión del clasificador, donde las filas representan la clase real y las columnas la clase predicha por el modelo:

|     |     |     |     |
| --- | --- | --- | --- |
| **Clase real / Clase predicha** | Enfermo(+) predicho | Sano(-) predicho | Total |
| Enfermo(+) | 35(VP) | 15(FN) | 50  |
| Sano(-) | 10(FP) | 40(VN) | 50  |
| Total | 45  | 55  | 100 |

El modelo identificó correctamente a 35 pacientes enfermos (verdaderos positivos) y a 40 pacientes sanos (verdaderos negativos). Sin embargo, clasificó incorrectamente a 15 pacientes enfermos como sanos (falsos negativos) y a 10 pacientes sanos como enfermos (falsos positivos).

b) Para el desarrollo de las métricas se utilizarán los valores obtenidos de la matriz de confusión:

- Verdaderos Positivos (VP) = 35
- Verdaderos Negativos (VN) = 40
- Falsos Positivos (FP) = 10
- Falsos Negativos (FN) = 15
- Total de observaciones (N) = 100

**Exactitud(Acuraccy):** La exactitud mide la proporción total de clasificaciones correctas realizadas por el modelo.

El modelo clasifica correctamente al 75% de los pacientes.

**Tasa de error:** La tasa de error representa la proporción de predicciones incorrectas.

El 25% de las clasificaciones realizadas por el modelo son incorrectas.

**Precisión :** La precisión indica qué proporción de los pacientes predichos como enfermos realmente lo están.

Cuando el modelo predice que un paciente está enfermo, acierta aproximadamente en el 78% de los casos.

**Sensibilidad (Recall):** La sensibilidad mide la capacidad del modelo para detectar correctamente a los pacientes enfermos.

El modelo detecta correctamente el 70% de los pacientes que realmente padecen la enfermedad.

**Especificidad:** La especificidad mide la capacidad del modelo para identificar correctamente a los pacientes sanos.

El modelo clasifica correctamente como sanos al 80% de los pacientes que realmente no tienen la enfermedad.

**Medida F1:** La medida F1 indica qué tan bien el modelo logra simultáneamente identificar correctamente los casos positivos y evitar falsas alarmas. Al combinar precisión y sensibilidad en un único valor, penaliza los casos en los que una de estas métricas es alta y la otra es baja.

En este caso, un valor de 73,68% muestra que el modelo posee un desempeño aceptable y relativamente equilibrado entre la detección de pacientes enfermos y la confiabilidad de sus predicciones positivas.

c) El coeficiente Kappa de Cohen es una medida estadística que cuantifica el grado de concordancia entre dos clasificaciones, ajustando el efecto del azar en la proporción de acuerdos observados. El estadístico kappa considera la posibilidad de que parte de la concordancia se produzca de manera aleatoria, proporcionando una evaluación más robusta del desempeño del modelo.

La fórmula es la siguiente:

- Po = acuerdo observado.
- Pe​ = acuerdo esperado por azar.

**Cálculo del acuerdo observado**

El acuerdo observado coincide con la accuracy del modelo, en este caso sería igual a lo siguiente:

**Cálculo del acuerdo esperado por azar**

Se calculan las proporciones marginales:

- Enfermos reales(ER): 50/100=0,50
- Sanos reales(SR): 50/100=0,50
- Enfermos predichos(EP): 45/100=0,45
- Sanos predichos(SP): 55/100​=0,55

Por lo tanto:

El calculo del estadístico Kappa seria el siguiente:

Como el estadístico Kappa es igual a 0,50 puede concluirse que el modelo logra un nivel de concordancia moderado, superior al que se obtendría por simple azar, aunque todavía existe margen para mejorar su capacidad de clasificación.

d) La métrica que se debe priorizar es la sensibilidad (recall), ya que mide la capacidad del modelo para identificar correctamente a los pacientes que realmente están enfermos. En este contexto, su importancia radica en que permite evaluar qué tan eficaz es el modelo para evitar falsos negativos. Por lo tanto, al momento de seleccionar el modelo, se prioriza el recall, dado que es la métrica que mejor refleja la capacidad de reducir este tipo de error, el cual es el más crítico desde el punto de vista en un contexto médico.

**Parte C. Sobreajuste**

**Ejercicio 5. Diagnóstico del sobreajuste**

a) A continuación se presenta un gráfico en el que se representan las curvas de error de entrenamiento y de validación en función de la complejidad del modelo, medida a través del número de nodos hoja del árbol de decisión.

b) A partir de las curvas obtenidas, se observa una región de subajuste en los modelos de menor complejidad (entre 1 y 5 nodos hoja), donde ambos errores son relativamente altos. Por otro lado, el sobreajuste comienza a evidenciarse a partir de los 15 nodos hoja, ya que el error de entrenamiento sigue disminuyendo mientras que el de validación aumenta. La complejidad óptima corresponde a 9 nodos hoja, dado que presenta el menor error de validación (0,19).

A continuación, se presenta el gráfico donde se indican las regiones de subajuste y sobreajuste, así como el punto de complejidad óptima, correspondiente al mínimo error de validación.

c) El error de entrenamiento decrece de forma monótona porque, al aumentar la complejidad del modelo, este dispone de una mayor capacidad para ajustarse a los datos de entrenamiento. En cambio, el error de validación presenta una curva en U, ya que inicialmente disminuye al capturar mejor los patrones de los datos, pero luego aumenta debido al sobreajuste, lo que reduce la capacidad de generalización del modelo.

d) Se seleccionaría el modelo con 9 nodos hoja, ya que presenta el menor error de validación (0,19). Esto indica que es el modelo con mejor capacidad de generalización, logrando un equilibrio adecuado entre el ajuste a los datos de entrenamiento y el desempeño sobre datos no vistos.

**Ejercicio 6. Poda mediante el error pesimista**

a) Antes de la división, el nodo se clasifica según la clase mayoritaria ("+"), generando 12 errores sobre 40 instancias, por lo que el error de entrenamiento es 0,30. Luego de la división, cada hoja se clasifica según su clase mayoritaria, obteniéndose un total de 11 errores sobre 40 instancias. En consecuencia, el error de entrenamiento pasa a ser 0,275. Por lo tanto, la división produce una reducción del error de entrenamiento de 0,025.

b) Previo a la división, el error de generalización pesimista es 0,3125. Después de la división, considerando la penalización de 0,5 por cada una de las cuatro hojas, el error pesimista resulta 0,325. Aunque la división reduce el error de entrenamiento, el incremento en la complejidad del árbol provoca un aumento del error pesimista. Por lo tanto, según este criterio, la división no estaría justificada y el nodo debería permanecer sin dividirse.

c) Sí, el subárbol debería podarse, ya que el error pesimista aumenta de 0,3125 a 0,325 después de la división. Esto indica que la mayor complejidad del subárbol no mejora la capacidad de generalización del modelo.

d) Este procedimiento está relacionado con el principio de parsimonia o navaja de Occam, que establece que, entre varias soluciones con desempeño similar, debe preferirse la más simple. En el contexto de los árboles de decisión, la poda busca eliminar divisiones que aumentan la complejidad del modelo sin aportar una mejora significativa en su capacidad de generalización. De este modo, se favorecen árboles más simples, menos propensos al sobreajuste y más fáciles de interpretar.

**Ejercicio 7. Estrategias de control del sobreajuste**

a)La pre-poda consiste en detener el crecimiento del árbol antes de que se complete, utilizando criterios que limitan su complejidad. Su principal ventaja es que reduce el costo computacional y evita la generación de árboles excesivamente grandes. Como desventaja, puede detener el crecimiento prematuramente y perder información relevante.

La post-poda consiste en generar primero el árbol completo y luego eliminar aquellas ramas que no contribuyen significativamente a la capacidad de generalización. Su ventaja es que suele producir modelos más precisos, ya que evalúa el árbol completo antes de simplificarlo. Como desventaja, requiere un mayor costo computacional.

b)Tres criterios de pre-poda utilizados habitualmente son:

- Establecer una profundidad máxima del árbol.
- Exigir un número mínimo de instancias para dividir un nodo.
- Requerir una ganancia mínima de información (o reducción mínima de impureza) para realizar una división.

c) La afirmación no es necesariamente correcta. Un árbol que clasifica correctamente el 100 % de los datos de entrenamiento puede haber aprendido no solo los patrones relevantes, sino también el ruido presente en dichos datos. Este fenómeno se conoce como sobreajuste (overfitting). Por lo tanto, un error de entrenamiento nulo no garantiza una buena capacidad de generalización; para evaluar la calidad del modelo es necesario analizar su desempeño sobre datos no utilizados durante el entrenamiento.

d) La validación cruzada de k pliegues divide el conjunto de datos en k subconjuntos. En cada iteración, uno de ellos se utiliza para validación y los restantes para entrenamiento. El proceso se repite k veces, utilizando cada subconjunto como conjunto de validación una vez, y el error final se obtiene promediando los resultados.

Este método permite obtener una estimación más robusta del error de generalización, ya que todas las observaciones participan tanto en entrenamiento como en validación. Cuando se dispone de pocos datos, resulta preferible a una única partición holdout, porque aprovecha mejor la información disponible y reduce la dependencia de una única división de los datos.


**Parte D. Clasificadores basados en reglas**

**Ejercicio 8. Derivación de reglas a partir de un árbol de decisión**

*(pendiente)*

**Ejercicio 9. Conjunto ordenado de reglas frente a votación**

a) La clasificación de cada transacción bajo los dos esquemas se presenta en la siguiente tabla:

|     |     |     |     |
| --- | --- | --- | --- |
| **Transacción** | **Reglas satisfechas** | **Conjunto ordenado (R1 > R2 > R3 > R4)** | **Votación no ponderada** |
| T1 | R1 → Fraude; R2 → Fraude | Fraude (R1, primera coincidencia) | Fraude (2 votos Fraude, 0 Legítima) |
| T2 | R2 → Fraude; R3 → Legítima; R4 → Legítima | Fraude (R2 precede a R3 y R4) | Legítima (1 voto Fraude, 2 votos Legítima) |
| T3 | Ninguna regla específica | Legítima (regla por defecto) | Legítima (regla por defecto) |

b) Los dos esquemas difieren únicamente en la transacción T2. En el conjunto ordenado, R2 (HoraInusual = Sí → Fraude) precede a R3 (Monto = Bajo → Legítima) y a R4 (ClienteAntiguo = Sí → Legítima) en el orden de prioridades; al satisfacerse el antecedente de R2, la clasificación se detiene y T2 recibe la clase Fraude sin evaluar las reglas restantes. En el esquema de votación, las tres reglas cuyo antecedente se satisface emiten su voto de forma independiente: R2 aporta un voto a Fraude, mientras que R3 y R4 aportan un voto cada una a Legítima; la clase mayoritaria (2 contra 1) determina el resultado final como Legítima.

c) El esquema de **conjunto ordenado** tiene como ventaja su eficiencia: la clasificación se detiene al encontrar la primera regla cuyo antecedente se satisface, sin necesidad de evaluar el resto. Su desventaja principal es que el orden de las reglas es determinante: una regla general ubicada antes que una más específica puede anularla, aun cuando la más específica sea más precisa para ese caso particular.

El esquema de **votación no ponderada** tiene como ventaja su robustez: al considerar todas las reglas aplicables de forma simultánea, el impacto de una regla individualmente incorrecta queda atenuado por las restantes. Su desventaja es el mayor costo computacional, dado que cada transacción debe ser evaluada contra la totalidad de las reglas antes de emitir una decisión.

**Ejercicio 10. Generación directa de reglas: cobertura secuencial**

a) El algoritmo de cobertura secuencial construye un conjunto de reglas de forma iterativa. En cada iteración, se busca la regla que mejor cubra instancias de la clase objetivo sin incluir instancias de otras clases, maximizando una medida de calidad como la precisión o la estimación de Laplace. Una vez identificada la regla, las instancias cubiertas se eliminan del conjunto de entrenamiento y el proceso se repite. El ciclo continúa hasta que todas las instancias de la clase objetivo han sido cubiertas o se alcanza un criterio de detención. Al finalizar, una regla por defecto asigna la clase mayoritaria a las instancias no cubiertas por ninguna regla específica (Tan et al., 2019).

b) Los puntos del Conjunto de Datos 3 se distribuyen de la siguiente manera:

- Clase "+": P1(1,1), P2(1,3), P3(2,2), P4(2,4), P5(6,1)
- Clase "−": P6(4,4), P7(5,5), P8(5,3), P9(3,5), P10(6,5)

**Iteración 1.** La condición x1 ≤ 2 cubre P1, P2, P3 y P4, todos de clase "+", sin incluir ningún punto de clase "−" (todos los negativos tienen x1 ≥ 3). Se incorpora la primera regla:

**R1: SI x1 ≤ 2 → clase "+"**

Se eliminan P1, P2, P3 y P4. Positivos restantes: {P5(6,1)}.

**Iteración 2.** La condición x2 ≤ 1 cubre P5(6,1) sin incluir ningún negativo (todos tienen x2 ≥ 3). Se incorpora la segunda regla:

**R2: SI x2 ≤ 1 → clase "+"**

No quedan positivos sin cubrir. El algoritmo concluye.

El conjunto de reglas resultante es:

- R1: SI x1 ≤ 2 → clase "+"
- R2: SI x2 ≤ 1 → clase "+"
- Regla por defecto: clase "−"

c) La construcción requirió dos reglas. Si se permitieran reglas con cobertura muy baja —por ejemplo, una sola instancia por regla— el algoritmo podría generar tantas reglas como instancias positivas existan, memorizando el conjunto de entrenamiento en lugar de capturar los patrones subyacentes. Este fenómeno se conoce como sobreajuste (*overfitting*): el clasificador resultante tendría buen desempeño sobre los datos de entrenamiento pero escasa capacidad de generalización frente a instancias nuevas. Además, un número elevado de reglas excesivamente específicas reduce la interpretabilidad del modelo y dificulta su mantenimiento.

**Parte E. Preguntas teóricas de desarrollo**

**1.** La diferencia fundamental entre el aprendizaje supervisado y el no supervisado radica en la disponibilidad de etiquetas de clase durante el entrenamiento. En el aprendizaje supervisado, cada instancia del conjunto de entrenamiento está asociada a una etiqueta conocida, y el modelo aprende a mapear instancias a salidas mediante la minimización de un error sobre dichos ejemplos etiquetados (Tan et al., 2019). En el aprendizaje no supervisado no se dispone de etiquetas; el objetivo consiste en descubrir estructura latente en los datos, tal como agrupamientos naturales (*clustering*) o patrones de co-ocurrencia (reglas de asociación).

La clasificación es una tarea de aprendizaje supervisado: a partir de un conjunto de instancias etiquetadas, se induce un modelo capaz de predecir la clase de nuevas instancias no vistas durante el entrenamiento. La variable de salida es discreta y categórica, lo que distingue a la clasificación de la regresión, cuya salida es continua.

**2.** El error de resustitución evalúa el modelo sobre el mismo conjunto de datos empleado para su entrenamiento, lo que permite al modelo memorizar instancias particulares —incluyendo el ruido— en lugar de aprender los patrones generalizables subyacentes. Este fenómeno se denomina sobreajuste. Un árbol completamente expandido sin poda puede alcanzar un error de resustitución nulo y al mismo tiempo exhibir un error de generalización elevado sobre datos no vistos (Tan et al., 2019). En consecuencia, el error de resustitución constituye un estimador optimista y sesgado del desempeño real del modelo; para obtener una estimación confiable del error de generalización es necesario evaluarlo sobre datos independientes del entrenamiento, por ejemplo mediante un conjunto de prueba o mediante validación cruzada.

**3.** Las tres medidas de impureza más empleadas en la inducción de árboles de decisión difieren en su sensibilidad a las distribuciones de clase:

- **Error de clasificación:** 1 − max_c p(c|t). Es simple pero poco sensible a cambios en las probabilidades de clase, dado que solo considera la clase más frecuente.
- **Entropía:** −Σ_c p(c|t) log₂ p(c|t). Penaliza con mayor intensidad las distribuciones uniformes y resulta más sensible a cambios en las clases minoritarias.
- **Índice de Gini:** 1 − Σ_c p(c|t)². De comportamiento similar a la entropía, es computacionalmente eficiente y constituye el criterio preferido en algoritmos tipo CART.

La ganancia de información —basada en la entropía— tiende a favorecer atributos con muchos valores distintos porque la partición en numerosos subconjuntos pequeños puede producir nodos aparentemente puros, aunque estos sean demasiado específicos para generalizar. La razón de ganancia (*gain ratio*) corrige este sesgo dividiendo la ganancia por la información de la partición (*split information*), que es la entropía de la distribución de instancias entre las ramas del atributo; de este modo, se penalizan los atributos que generan un número elevado de ramas (Tan et al., 2019).

**4.** Los árboles de decisión presentan las siguientes ventajas principales como clasificadores:

- **Interpretabilidad:** la estructura del árbol se traduce directamente en reglas SI–ENTONCES legibles sin necesidad de formación técnica en aprendizaje automático.
- **Ausencia de requisitos de preprocesamiento:** no requieren normalización ni estandarización de atributos y admiten de forma nativa tanto variables categóricas como continuas.
- **Robustez frente a atributos irrelevantes:** los atributos que no aportan ganancia de información no son seleccionados para ninguna partición y no afectan el modelo.

Entre sus principales limitaciones se destacan:

- **Propensión al sobreajuste:** sin mecanismos de poda, los árboles completamente expandidos memorizan los datos de entrenamiento y generalizan de forma deficiente.
- **Inestabilidad:** pequeñas variaciones en el conjunto de entrenamiento pueden producir árboles estructuralmente muy distintos, dado que la selección del atributo raíz condiciona toda la estructura posterior.
- **Fronteras de decisión paralelas a los ejes:** cada partición considera un único atributo, por lo que las fronteras diagonales o curvas solo pueden aproximarse mediante un número elevado de divisiones consecutivas, lo que incrementa la complejidad del modelo.

**5.** El error esperado de generalización de un modelo se descompone en tres componentes: el ruido irreducible del problema, el sesgo al cuadrado y la varianza. El **sesgo** cuantifica el error sistemático introducido por las suposiciones simplificadoras del modelo; un modelo con sesgo elevado clasifica erróneamente de forma consistente independientemente del conjunto de entrenamiento utilizado. La **varianza** cuantifica la sensibilidad del modelo a las fluctuaciones en los datos de entrenamiento; un modelo con varianza elevada ajusta los datos de entrenamiento en detalle pero generaliza de forma deficiente (Tan et al., 2019).

El **subajuste** corresponde a la combinación de sesgo elevado y varianza baja: el modelo es demasiado simple para capturar los patrones relevantes y comete errores altos tanto en entrenamiento como en validación. El **sobreajuste** corresponde a sesgo bajo y varianza elevada: el modelo se ajusta en exceso a los datos de entrenamiento, capturando el ruido, y su desempeño se degrada sobre datos no vistos. La complejidad óptima minimiza la suma de sesgo² y varianza, maximizando la capacidad de generalización del modelo.

**6.** Desde el punto de vista de la **expresividad**, un clasificador basado en reglas generado mediante cobertura secuencial puede ser más expresivo que un árbol de decisión, dado que cada regla no está condicionada por la jerarquía de particiones establecida en los nodos superiores. Cada regla puede capturar una región del espacio de instancias de forma independiente, sin necesidad de subdividir todo el espacio (Tan et al., 2019).

En cuanto a la **interpretabilidad**, ambas representaciones son intrínsecamente legibles. No obstante, las reglas individuales pueden ser más fáciles de evaluar en forma aislada por expertos de dominio, quienes pueden validar cada condición sin necesidad de recorrer una estructura jerárquica completa.

Respecto a la **facilidad de mantenimiento**, los clasificadores basados en reglas presentan una ventaja clara: es posible agregar, modificar o eliminar reglas individuales sin reconstruir el modelo completo. En un árbol de decisión, la modificación de una partición en un nodo interno de alta jerarquía afecta la estructura de todos los subárboles dependientes, lo que hace más costosa cualquier actualización incremental del modelo.

**7.** El desbalance de clases se produce cuando la distribución de instancias entre clases es marcadamente asimétrica, como ocurre en la detección de fraude o en el diagnóstico de enfermedades poco frecuentes. En ese contexto, la exactitud resulta una métrica inadecuada porque un clasificador trivial que predice siempre la clase mayoritaria obtiene valores elevados de exactitud sin poseer capacidad discriminativa alguna (Tan et al., 2019).

Entre las alternativas más apropiadas se encuentran:

- La **sensibilidad** (*recall*) y la **precisión**, que focalizan la evaluación en el desempeño sobre la clase minoritaria.
- La **medida F1**, que armoniza ambas métricas en un único valor.
- El **estadístico Kappa de Cohen**, que ajusta el acuerdo observado por el efecto del azar.
- El **área bajo la curva ROC (AUC-ROC)**, que evalúa la capacidad discriminativa del modelo en todos los umbrales de clasificación posibles.
- Técnicas de **remuestreo**, como el sobremuestreo de la clase minoritaria (por ejemplo, mediante SMOTE) o el submuestreo de la clase mayoritaria, con el fin de rebalancear el conjunto de entrenamiento antes de la inducción del modelo.

**8.** Aunque un clasificador basado en reglas y un árbol de decisión pueden representar el mismo conocimiento, cada representación resulta preferible en distintos contextos.

El **árbol de decisión** es preferible cuando el proceso de decisión es inherentemente jerárquico —es decir, cuando las decisiones tempranas condicionan las posteriores— y cuando el objetivo es visualizar la lógica de clasificación completa en una única estructura compacta. También resulta adecuado cuando se requiere auditar el proceso de decisión de forma integral, ya que el árbol expone simultáneamente todas las trayectorias posibles de clasificación.

El **clasificador basado en reglas** es preferible cuando distintos subconjuntos del espacio de instancias siguen patrones independientes que no pueden organizarse de forma natural en una jerarquía sin introducir particiones redundantes o artificiales. Asimismo, las reglas son más apropiadas cuando la lógica de clasificación debe comunicarse a expertos de dominio que evalúan criterios en forma individual —como en protocolos de diagnóstico médico— o cuando el modelo debe actualizarse de manera incremental mediante la incorporación, modificación o eliminación de reglas sin afectar el resto del clasificador.
