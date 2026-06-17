> Introducción a Data Mining — Trabajo Práctico de Clasificación
>
> **Universidad** **Austral** Maestría en Ciencia de Datos
>
> Asignatura: Introducción a Data Mining
>
> **Trabajo** **Práctico**

**Clasificación:** **árboles** **de** **decisión,** **clasificadores**
**basados** **en** **reglas** **y** **sobreajuste**

> Modalidad: trabajo individual o en grupos
>
> Partes A a E: resolución manuscrita. Parte F: resolución empleando
> software
>
> Página 1
>
> Introducción a Data Mining — Trabajo Práctico de Clasificación

**1.** **Presentación** **y** **encuadre**

El presente Trabajo Práctico integra los contenidos de la asignatura,
dedicados a la clasificación. Su propósito es que el estudiante
consolide, mediante la resolución de problemas, los fundamentos de la
inducción de árboles de decisión, la evaluación de clasificadores, el
diagnóstico y el control del sobreajuste, y la construcción de
clasificadores basados en reglas. El trabajo combina ejercicios de
cálculo manual, preguntas teóricas de desarrollo y un componente
práctico de implementación en R o en el lenguaje o herramienta de su
preferencia.

**1.1.** **Objetivos** **de** **aprendizaje**

Al finalizar el Trabajo Práctico, el estudiante será capaz de:

> • Calcular medidas de impureza de nodos (índice de Gini y entropía) y
> la ganancia de información, y emplearlas como criterio de selección de
> atributos de partición.
>
> • Inducir árboles de decisión manualmente a partir de conjuntos de
> datos de tamaño
>
> reducido.
>
> • Determinar los puntos de corte óptimos para atributos continuos.
>
> • Construir e interpretar la matriz de confusión y las métricas de
> desempeño derivadas de
>
> ella.
>
> • Diagnosticar el sobreajuste y aplicar estrategias de poda y de
> control de la complejidad
>
> del modelo.
>
> • Derivar, evaluar y aplicar clasificadores basados en reglas, tanto a
> partir de árbolescomo
>
> mediante métodos directos.
>
> • Implementar, evaluar y comparar árboles de decisión y clasificadores
> de reglas en R.

**1.2.** **Modalidad** **de** **trabajo** **y** **entrega**

El Trabajo Práctico puede resolverse de forma individual o en grupos.
Las Partes A a E deben resolverse “a mano”, exhibiendo la totalidad de
los cálculos y las justificaciones; no se admiten respuestas sin
desarrollo. La Parte F debe resolverse en R o con el software de su
preferencia, y entregarse como un script reproducible (archivo .R) o
como un documento R Markdown (.Rmd), acompañado deuninforme en formato
PDF que incluya el código, las salidas relevantes y la discusión de los
resultados. El plazo de entrega será definido por la cátedra.

> Página 2
>
> Introducción a Data Mining — Trabajo Práctico de Clasificación

**1.3.** **Criterios** **de** **evaluación**

La calificación se compondrá de los siguientes criterios: corrección de
los cálculos y procedimientos (40 %); justificación e interpretación de
los resultados (30 %); calidad del código y reproducibilidad de la Parte
F (20 %); y claridad en la presentación y la redacción (10 %).

**1.4.** **Herramientas** **y** **conjuntos** **de** **datos**

Para la Parte F se utilizará R (versión 4.3 o superior) con los paquetes
rpart, rpart.plot, caret, C50 y mlbench, en línea con el R Companion de
la asignatura (Hahsler, 2025). Todos los conjuntos de datos necesarios
para las Partes A a E se incluyen en el presente enunciado.

> Página 3
>
> Introducción a Data Mining — Trabajo Práctico de Clasificación

**Parte** **A.** **Árboles** **de** **decisión:** **impureza** **e**
**inducción**

El Conjunto de Datos 1 (Tabla 1) registra 14 solicitudes de crédito.
Cada solicitud se describe mediante tres atributos predictores (Ingreso,
Historial crediticio y Deuda) y el atributo de clase Otorga, que indica
si se otorgó el crédito.

> *Tabla* *1.* *Conjunto* *de* *Datos* *1* *—* *Solicitudes* *de*
> *crédito.*

||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||

**Ejercicio** **1.** **Medidas** **de** **impureza** **y** **selección**
**del** **atributo** **raíz** Con base en el Conjunto de Datos 1:

> **a)** Calcule la entropía y el índice de Gini del nodo raíz, es
> decir, antes de realizar cualquier partición.
>
> **b)** Para cada uno de los tres atributos candidatos (Ingreso,
> Historial y Deuda), calcule la entropía ponderada de los nodos hijos y
> la ganancia de información correspondiente.
>
> **c)** Calcule asimismo el índice de Gini ponderado de cada atributo
> candidato y la reducción de la impureza de Gini que este produce.
>
> **d)** Indique qué atributo seleccionaría como raíz del árbol según la
> ganancia de información. ¿Coincide la elección con la que indicaría el
> índice de Gini? Justifique su respuesta.
>
> Página 4
>
> Introducción a Data Mining — Trabajo Práctico de
> Clasificación<img src="./nvtnughq.png"
> style="width:6.265in;height:0.25167in" />

**Ejercicio** **2.** **Inducción** **del** **árbol** **de** **decisión**
**completo**

A partir del atributo raíz seleccionado en el Ejercicio 1, continúe la
inducción del árbol de decisiónde manerarecursiva, empleando
lagananciadeinformación como criterio departición, hasta que todos los
nodos hoja sean puros o no queden atributos disponibles.

> **a)** Dibuje el árbol de decisión resultante. En cada nodo interno
> indique el atributo de partición y, en cada hoja, la clase predicha
> junto con la cantidad de instancias que contiene.
>
> **b)** Exprese el árbol en forma de pseudocódigo, mediante una
> estructura de reglas anidadas “**si…** **entonces…**”.
>
> **c)** ¿Cuántos nodos hoja tiene el árbol? ¿Cuál es su error de
> resustitución, es decir, su error sobre el propio conjunto de
> entrenamiento?

**Ejercicio** **3.** **Partición** **de** **un** **atributo**
**continuo**

El Conjunto de Datos 2 (Tabla 2) contiene 10 registros caracterizados
por un atributo continuo, el Ingreso imponible (expresado en miles de
pesos), y por el atributo de clase Evade, que indica si el contribuyente
evade impuestos.

> *Tabla* *2.* *Conjunto* *de* *Datos* *2* *—* *Ingreso* *imponible* *y*
> *evasión* *(registros* *ordenados* *por* *ingreso).*
>
> **a)** Enumere los puntos de corte candidatos, definidos como los
> puntos medios de los valores consecutivos del atributo ordenados.
>
> **b)** Para cada punto de corte candidato, calcule el índice de Gini
> ponderado de la partición binaria resultante.
>
> **c)** Indique el punto de corte óptimo y exprese la condición de
> prueba asociada al nodo.
>
> **d)** Explique por qué los árboles de decisión solo generan fronteras
> de decisión paralelas a los ejes de coordenadas.
>
> Página 5
>
> Introducción a Data Mining — Trabajo Práctico de Clasificación

**Parte** **B.** **Evaluación** **de** **clasificadores** **Ejercicio**
**4.** **Matriz** **de** **confusión** **y** **métricas** **de**
**desempeño**

Un clasificador binario fue evaluado en un conjunto de prueba de 100
pacientes para detectar una enfermedad. Se define como clase positiva
“Enfermo” y como clase negativa “Sano”. El modelo produjo 35 verdaderos
positivos, 15 falsos negativos, 10 falsos positivos y 40 verdaderos
negativos.

> **a)** Construya la matriz de confusión correspondiente, identificando
> claramente la clase real y la predicha.
>
> **b)** Calcule la exactitud, la tasa de error, la precisión, la
> sensibilidad (recall), la especificidad y la medida F1.
>
> **c)** Calcule el estadístico kappa de Cohen e interprete su valor.
>
> **d)** Suponga que un falso negativo (no detectar a un paciente
> efectivamente enfermo) acarrea un costo mucho mayor que un falso
> positivo. ¿Qué métrica priorizaría para seleccionar el modelo?
> Justifique.
>
> Página 6
>
> Introducción a Data Mining — Trabajo Práctico de Clasificación

**Parte** **C.** **Sobreajuste**

**Ejercicio** **5.** **Diagnóstico** **del** **sobreajuste**

La Tabla 3 presenta el error de un árbol de decisión sobre el conjunto
de entrenamiento y sobre un conjunto de validación independiente, en
función de la complejidad del modelo, medida como el número de nodos
hoja.

> *Tabla* *3.* *Error* *de* *entrenamiento* *y* *de* *validación*
> *según* *la* *complejidad* *del* *modelo.*

||
||
||
||
||
||
||
||
||
||
||

> **a)** Represente gráficamente ambas curvas de error en función de la
> complejidad del modelo, en un mismo sistema de ejes.
>
> **b)** Identifique las regiones de subajuste y de sobreajuste, y
> señale la complejidad óptima.
>
> **c)** Explique por qué el error de entrenamiento decrece de forma
> monótona, mientras que el error de validación describe una curva en U.
>
> **d)** ¿Qué complejidad de modelo seleccionaría? Justifique su
> elección en términos del error de generalización.

**Ejercicio** **6.** **Poda** **mediante** **el** **error**
**pesimista**

Considereel subárboldescritoa continuación: unnodo internocontiene40
instancias del conjunto de entrenamiento, de las cuales 28 pertenecen a
la clase “+” y 12 a la clase “–“. Dicho nodo se divide en cuatro nodos
hoja, cuyas distribuciones de clase se detallan en la Tabla 4.

> *Tabla* *4.* *Distribución* *de* *clases* *en* *los* *nodos* *hoja*
> *del* *subárbol* *del* *Ejercicio* *6.*

||
||
||
||
||
||
||

> **a)** Calcule el error de entrenamiento del nodo antes de la división
> (tratándolo como hoja) y después de la división.
>
> Página 7
>
> Introducción a Data Mining — Trabajo Práctico de Clasificación
>
> **b)** Calcule el error de generalización pesimista antes y después de
> la división, penalizando cada nodo hoja con un factor de 0,5. Recuerde
> que el error pesimista se define como *(errores* *+* *k* *·* *0,5)*
> */* *N*, donde k es el número de hojas y N el número de instancias.
>
> **c)** A partir de la comparación de los errores pesimistas, ¿debería
> podarse el subárbol? Justifique su respuesta.
>
> **d)** ¿Qué relación tiene este procedimiento con el principio de
> parsimonia, conocido como la navaja de Occam?

**Ejercicio** **7.** **Estrategias** **de** **control** **del**
**sobreajuste** Responda de forma fundamentada a las siguientes
consignas:

> **a)** Distinga la pre-poda (detención temprana) de la post-poda.
> Indique una ventaja y una desventaja de cada estrategia.
>
> **b)** Mencione tres criterios de pre-poda que se utilicen
> habitualmente en la inducción de árboles de decisión.
>
> **c)** Un colega afirma: *“Mi* *árbol* *clasifica* *correctamente*
> *el100* *%de* *losdatosde* *entrenamiento,* *por* *lo* *tanto,* *es*
> *un* *excelente* *modelo”*. Critique esta afirmación de manera
> rigurosa.
>
> **d)** Explique cómo la validación cruzada de k pliegues permite
> estimar el error de generalización y por qué resulta preferible a una
> única partición de retención (holdout) cuando se dispone de pocos
> datos.
>
> Página 8
>
> Introducción a Data Mining — Trabajo Práctico de Clasificación

**Parte** **D.** **Clasificadores** **basados** **en** **reglas**

**Ejercicio** **8.** **Derivación** **de** **reglas** **a** **partir**
**de** **un** **árbol** **de** **decisión**

Considere el árbol de decisión obtenido en el Ejercicio 2, inducido
sobre el Conjunto de Datos 1.

> **a)** Derive el conjunto completo de reglas de clasificación,
> recorriendo cada camino desde la raíz hasta una hoja.
>
> **b)** Para cada regla, indique su cobertura —la cantidad de
> instancias del Conjunto de Datos 1 que satisface su antecedente— y su
> exactitud sobre dichas instancias.
>
> **c)** ¿El conjunto de reglas resultante es mutuamente excluyente y
> exhaustivo? Justifique su respuesta.
>
> **d)** Clasifique los siguientes solicitantes nuevos: **S1** (Ingreso
> = Medio, Historial = Malo, Deuda = Baja) y **S2** (Ingreso = Bajo,
> Historial = Bueno, Deuda = Alta).

**Ejercicio** **9.** **Conjunto** **ordenado** **de** **reglas**
**frente** **a** **votación**

Un sistema antifraude clasifica las transacciones como “Fraude” o
“Legítima” mediante el siguiente conjunto de reglas:

R1: (Monto = Alto) Y (PaisDistinto = Si) -\> Fraude R2: (HoraInusual =
Si) -\> Fraude

R3: (Monto = Bajo) -\> Legitima R4: (ClienteAntiguo = Si) -\> Legitima
Regla por defecto -\> Legitima

Clasifique las tres transacciones de la Tabla 5 bajo dos esquemas: (i)
un conjunto ordenado de reglas, es decir, una lista de decisión con
prioridad R1 \> R2 \> R3 \> R4; y (ii) una votación no ponderada de
todas las reglas cuyo antecedente se satisface.

> *Tabla* *5.* *Transacciones* *a* *clasificar* *en* *el* *Ejercicio*
> *9.*

||
||
||
||
||
||

> **a)** Indique la clase asignada a cada transacción en cada uno de los
> dos esquemas.
>
> **b)** Señale en qué transacciones difieren los resultados de ambos
> esquemas y explique la causa de la discrepancia.
>
> **c)** Discuta una ventaja y una desventaja de cada esquema de
> resolución de conflictos entre reglas.
>
> Página 9
>
> Introducción a Data Mining — Trabajo Práctico de
> Clasificación<img src="./ud3ffjvp.png"
> style="width:6.26917in;height:0.25167in" />

**Ejercicio** **10.** **Generación** **directa** **de** **reglas:**
**cobertura** **secuencial**

El Conjunto de Datos 3 (Tabla 6) contiene 10 puntos en un espacio
bidimensional, descritos por los atributos continuos x1 y x2, y
etiquetados con la clase “+” o “–“.

> *Tabla* *6.* *Conjunto* *de* *Datos* *3* *—* *Puntos* *en* *el*
> *plano* *para* *el* *Ejercicio* *10.*
>
> **a)** Describa, con sus propias palabras, el algoritmo de cobertura
> secuencial para la generación directa de reglas.
>
> **b)** Aplique el algoritmo para construir un conjunto de reglas que
> cubra la clase “+”. Cada regla debe expresarse como una conjunción de
> condiciones sobre x1 y x2 y no debe cubrir ningún punto de la clase
> “–“.
>
> **c)** Indique cuántas reglas fueron necesarias y discuta qué
> consecuencias tendría permitir reglas con una cobertura muy baja.
>
> Página 10
>
> Introducción a Data Mining — Trabajo Práctico de Clasificación

**Parte** **E.** **Preguntas** **teóricas** **de** **desarrollo**

Responda de forma clara, precisa y fundamentada. Se valorará el uso
correcto de la terminología técnica y la articulación de los conceptos.

> 1\. Explique la diferencia entre aprendizaje supervisado y no
> supervisado, y ubique la tarea de clasificación dentro de esta
> taxonomía.
>
> 2\. ¿Por qué el error de entrenamiento (error de resustitución) no
> constituye un estimador fiable del desempeño de un modelo sobre datos
> nuevos?
>
> 3\. Compare el índice de Gini, la entropía y el error de clasificación
> como medidas de impureza. ¿Por qué la ganancia de información tiende a
> favorecer los atributos con muchos valores y de qué modo lo corrige la
> razón de ganancia?
>
> 4\. Enuncie y justifique las principalesventajas y limitaciones de los
> árbolesde decisión como clasificadores.
>
> 5\. Explique el compromiso entre sesgo y varianza y relaciónelo con
> los fenómenos de subajuste y sobreajuste.
>
> 6\. Compare los clasificadores basados en reglas con los árboles de
> decisión en términos de expresividad, interpretabilidad y facilidad de
> mantenimiento.
>
> 7\. ¿En qué consiste el problema del desbalance de clases? ¿Por qué la
> exactitud resulta una métrica inadecuada en ese contexto y qué
> alternativas propondría?
>
> 8\. Un clasificador basado en reglas y un árbol de decisión pueden
> representar el mismo conocimiento. Discuta en qué situaciones
> preferiría cada una de las dos representaciones.
>
> Página 11
>
> Introducción a Data Mining — Trabajo Práctico de Clasificación

**Parte** **F.** **Práctica** **en** **R**

Esta parte se resuelve en R. Se utilizará el conjunto de datos
PimaIndiansDiabetes del paquete mlbench (768 observaciones; ocho
atributos predictores numéricos y el atributo de clase diabetes, con
valores pos y neg). El siguiente fragmento prepara el entorno de
trabajo:

pkgs \<- c("rpart","rpart.plot","caret","C50","mlbench")
install.packages(pkgs\[!(pkgs %in%
installed.packages()\[,"Package"\])\]) library(rpart);
library(rpart.plot); library(caret)

library(C50); library(mlbench) data(PimaIndiansDiabetes, package =
"mlbench") set.seed(2026)

**Ejercicio** **11.** **Árboles** **de** **decisión** **con** **rpart**

> **a)** Cargue los datos y particiónelos en un70% de entrenamientoy
> un30% de pruebamediante caret::createDataPartition. Fije la semilla
> del generador de números aleatorios para garantizar la
> reproducibilidad.
>
> **b)** Induzca un árbol de decisión sobre el conjunto de entrenamiento
> con la función rpart() y visualícelo con rpart.plot().
>
> **c)** Calcule el error de resustitución (sobre el conjunto de
> entrenamiento) y el error de generalización(sobreel
> conjuntodeprueba)mediante caret::confusionMatrix(). Compare ambos
> valores y comente.
>
> **d)** Informe la exactitud, la sensibilidad, la especificidad y el
> estadístico Kappa obtenidos sobre el conjunto de prueba.

**Ejercicio** **12.** **Sobreajuste** **y** **poda** **en** **R**

> **a)** Induzca un árbol «completo» fijando los hiperparámetros
> rpart.control(minsplit = 2, cp = 0) y compare su error de
> resustitución con su error de generalización. ¿Qué evidencia de
> sobreajuste observa?
>
> **b)** Utilice caret::train()convalidación cruzadade 10 pliegues para
> seleccionar el valor óptimo del parámetro de complejidad cp.
>
> **c)** Genere la curva del error estimado por validación cruzada en
> función de cp e interprétela.
>
> **d)** Compare el desempeño del árbol completo, el árbol por defecto y
> el árbol podado sobre el conjunto de prueba. Extraiga una conclusión.

**Ejercicio** **13.** **Clasificador** **basado** **en** **reglas**
**en** **R**

> **a)** Induzca un clasificador basado en reglas con el algoritmo C5.0
> (paquete C50), utilizando la opción rules = TRUE, sobre el mismo
> conjunto de entrenamiento del Ejercicio 11.
>
> **b)** Inspeccione el conjunto de reglas generado con summary() e
> interprete dos de las reglas obtenidas.
>
> **c)** Evalúe el clasificador de reglas sobre el conjunto de prueba y
> compare su desempeño con el del árbol de decisión del Ejercicio 11.
>
> Página 12
>
> Introducción a Data Mining — Trabajo Práctico de Clasificación

**d)** Discuta las diferencias de interpretabilidad entre el árbol de
decisión y el conjunto de reglas. Como alternativa, puede emplearse el
método "PART" mediante caret::train() con el paquete RWeka.

> Página 13
>
> Introducción a Data Mining — Trabajo Práctico de Clasificación

**Referencias**

Hahsler, M. (2025). *An* *R* *companion* *for* *Introduction* *to*
*Data* *Mining*. Recuperado de
https://mhahsler.github.io/Introduction_to_Data_Mining_R_Examples/

Hahsler, M. (2025). *Introduction* *to* *Data* *Mining* *—* *Lecture*
*slides* \[Material de cátedra\]. Basado en Tan, Steinbach, Karpatne y
Kumar. Licencia Creative Commons BY-SA 4.0.

Tan, P.-N., Steinbach, M., Karpatne, A., & Kumar, V. (2019).
*Introduction* *to* *data* *mining* (2.ª ed.). Pearson.

Therneau, T., & Atkinson, B. (2025). *rpart:* *Recursive* *partitioning*
*and* *regression* *trees* \[Paquete de R\].

Kuhn, M. (2024). *caret:* *Classification* *and* *regression* *training*
\[Paquete de R\].

> Página 14
