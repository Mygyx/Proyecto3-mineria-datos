# Bitácora del Proyecto III de Minería de Datos

Curso ISW-911 · Caso Grupo Innova S.A. · Python y Jupyter Notebook

Equipo: Miguel, Brian, Jeremy y Cristopher.

## Estado actual al 28 de noviembre de 2026

Revisión del trabajo local sobre `main` (`04b4daf)), comparado con el [enunciado del Proyecto III](Proyecto%20%23%203%20Minera%20de%20Datos.pdf). Los porcentajes corresponden a la rúbrica.

La última revisión del notebook guardado encontró 31 celdas de código con registro de ejecución y sin errores guardados. Los conteos de la tabla comparativa final coinciden con el CSV de predicciones.

| Tarea | Responsable | Estado | Resultados y evidencia |
| --- | --- | --- | --- |
| Pregunta de negocio y EDA, parte de Fase I (10 %) | Brian | Completado | Completos. Pregunta de recompra al mes siguiente vinculada al KPI-04. Perfil de 2.240 líneas, 412 facturas y 59 clientes, revisión de calidad, atípicos y correlaciones, y cuatro figuras de EDA. |
| Ingeniería y preparación, resto de Fase I | Brian y Jeremy | Completado | Completos. [Tabla cliente-mes](resultados/tablas/cliente_mes.csv) con 405 casos y 40 recompras, diccionario y controles de trazabilidad. Pipelines con imputación, codificación de país y escalado para logística. División por mes del resultado, con 325 casos de desarrollo y 80 de prueba. |
| Estratificación solicitada en la Fase I | Equipo, con Jeremy | Sin terminar | Faltantes. El PDF pide estratificar si hay desbalance. El notebook usa un corte cronológico para representar predicciones futuras y conservar los meses completos. Los pesos de clase son parte del ajuste y la proporción de positivos varía por año. Falta confirmar con el profesor si acepta esta justificación. Los resultados de 2013 se usaron para la comparación final y quedaron fuera del ajuste. |
| Ratificación de la pregunta | Equipo | Sin terminar | Faltantes. Hay una pregunta implementada, pero todavía no consta su ratificación por los cuatro integrantes. |
| Fase II. Modelado y entrenamiento (30 %) | Jeremy | Completado | Completos. Logística y árbol ajustados con tres bloques temporales de validación y comparados con una referencia mayoritaria. F1 positivo de validación de 0,3048 y 0,5484, respectivamente. Umbrales fijados en 0,10 y 0,50. El AUC anual de 2012 queda indefinido porque hubo cero recompras. [Protocolo](resultados/tablas/fase2_protocolo.json) · [Resumen de validación](resultados/tablas/fase2_resumen_validacion.csv). |
| Reproducibilidad de la entrega | Equipo | Verificada para las fases I a III | La ejecución en copia temporal reprodujo 16 CSV y generó 10 figuras con las dependencias instaladas. El README y el protocolo coinciden en Python 3.13.17. Queda alinear la guía de ejecución con el notebook, que incluye `%pip install matplotlib` entre las celdas de análisis. |
| Fase III. Evaluación, selección e importancia (20 %) | Miguel | Completado | Completos. Comparación sobre 80 casos de 2013, curvas ROC, matrices de confusión, predicciones por caso y análisis de errores. Se eligió la logística por F1 de recompra de 0,40, con seis de siete recompras detectadas y 17 falsas alarmas. El árbol tuvo el mayor AUC (0,8973) y emitió cero alertas con su umbral de 0,50. En validación de 2010 y 2011, el gasto de los últimos 90 días tuvo la mayor caída media de F1 por permutación (0,1621). |
| Fase IV. Impacto y recomendaciones (10 %) | Cristopher | Sin terminar | Faltantes. Hay tres propuestas y un guion en esta bitácora. Faltan tres decisiones sustentadas en los resultados finales y una presentación ejecutiva que traduzca las métricas a impacto operativo y muestre las variables más influyentes. Miguel calcula la importancia en su fase para que Cristopher la incorpore. |
| Defensa oral y dominio individual (30 %) | Equipo | No iniciado en el repositorio | Faltantes. Falta evidencia del ensayo de 20 minutos de exposición y 5 de preguntas técnicas individuales. |

### Autoría según los commits locales y las referencias disponibles

| Autor en Git | Commits | Avance registrado |
| --- | --- | --- |
| Miguel Cruz (Mygyx) | `8f991af`, `50e1fd7` | Commit inicial con el README (`8f991af`). Estructura del proyecto, CSV del workshop, investigación, plan de trabajo e introducción del notebook (`50e1fd7`). |
| Brian Rodriguez | `114d6a0`, `47f68b7`, `d980d5c`, `241f98a`, `b139ef6`, `6fd4151`, `f992a5f`, `4c4ee0d` | Carga y calidad, etiqueta cliente-mes, análisis de variables, controles y exportaciones, figuras, inclusión de diciembre de 2013, guía del kernel y actualización posterior del notebook que incorporó la celda de instalación. |
| jrodriguezes (Jeremy Rodriguez Esquivel) | `f1768c1`, `04b4daf` | Partición temporal, pipelines, ajuste, validación y exportaciones. Documentación de ejecución y del intercambio de fases con Miguel. |
| Cristopher | Sin commits identificados | Tiene asignadas las recomendaciones y la presentación. Git solo acredita aportes registrados bajo las identidades visibles. |

### Entrega de Miguel y siguiente paso

La [tabla comparativa](resultados/tablas/fase3_comparacion_prueba.csv) incluye las métricas, los aciertos sin recompra y las alertas totales. La logística obtuvo 56 aciertos sin recompra y 23 alertas. Los conteos se verificaron con las [240 predicciones de prueba](resultados/tablas/fase3_predicciones_prueba.csv). También quedaron guardadas la [tabla de importancia](resultados/tablas/fase3_importancia_logistica.csv), las [curvas ROC con los umbrales fijados](resultados/figuras/fase3_curvas_roc.png), las [matrices de confusión](resultados/figuras/fase3_matrices_confusion.png), la [gráfica mensual](resultados/figuras/fase3_desempeno_mensual_logistica.png) y la [gráfica de importancia](resultados/figuras/fase3_importancia_logistica.png).

El [notebook](notebooks/proyecto_3.ipynb) incluye una comparación exploratoria con un cupo común de 23 revisiones en 2013. El árbol priorizó las siete recompras observadas y la logística seis. La selección principal se mantiene por F1 con los umbrales fijados en la Fase II.

Miguel entrega estos resultados a Cristopher para que traduzca las 23 alertas, las seis recompras detectadas y las 17 falsas alarmas a implicaciones operativas y sustente las tres decisiones de la Fase IV. En la defensa, el F1 de 0,40 se presenta como el resultado observado en el mismo bloque de 2013 usado para comparar y elegir el modelo. El equipo aún debe documentar la ratificación de la pregunta y confirmar con el profesor si acepta el corte temporal.

## Estructura del repositorio

| Ruta | Uso |
| --- | --- |
| [README.md](README.md) | Estructura del repositorio y rutas de carga según el directorio de trabajo. |
| [data/](data/) | Contiene [data_process.csv](data/data_process.csv), el insumo procesado del workshop 4. |
| [proyecto_3.ipynb](notebooks/proyecto_3.ipynb) | Introducción y fases I a III ejecutadas. Incluye EDA, entrenamiento, comparación de 2013, análisis de errores e importancia de variables. |
| [resultados/figuras/](resultados/figuras/) | Gráficos exportados para comparación y defensa. |
| [resultados/tablas/](resultados/tablas/) | Tablas de EDA, datos cliente-mes, validación temporal, predicciones de 2013 e importancia por permutación. |
| [presentacion/](presentacion/) | Carpeta reservada para las diapositivas. Actualmente solo contiene `.gitkeep`. |
| [agentes.md](agentes.md) | Estado, decisiones y aportes del equipo. |

## Reparto actual

Brian Rodriguez es el responsable de la **Fase I**, Jeremy Rodriguez Esquivel de la **Fase II** y Miguel Cruz de la **Fase III**.

| Responsable | Trabajo principal | Entrega al equipo |
| --- | --- | --- |
| Brian | Fase I. Plantear la pregunta de negocio, justificar el objetivo, hacer EDA y definir qué variables están disponibles al predecir. | Tabla cliente-mes y diccionario. Diagnóstico de tipos, cardinalidad, faltantes, atípicos y correlaciones. Ratificación de la pregunta pendiente del equipo. |
| Jeremy | Fase II. Implementar la partición y el preprocesamiento reproducible. Entrenar y ajustar al menos dos algoritmos adecuados usando validación dentro de entrenamiento. | Modelos comparables, hiperparámetros justificados y flujo reproducible de codificación, escalado e imputación según corresponda. |
| Miguel | Fase III. Evaluar ambos modelos sobre la misma prueba independiente y justificar la selección. Analizar los errores y estimar la importancia de las variables del modelo elegido. | Tabla de métricas, figuras e interpretación técnica para la presentación. |
| Cristopher | Fase IV. Convertir las métricas y la importancia de variables en conclusiones de negocio. Preparar las diapositivas y coordinar el ensayo. | Presentación con impacto operativo y al menos tres decisiones estratégicas concretas derivadas de los resultados. |

Brian comunicó el intercambio de las fases I y II con Miguel el 23 de noviembre de 2026. Jeremy comunicó el intercambio de las fases II y III con Miguel el 24 de noviembre de 2026. Los cuatro acuerdan el objetivo y el esquema de validación antes de modelar. Cada integrante revisa el notebook completo y practica explicar el código, la teoría y las decisiones de las cuatro fases.

## KPIs y decisión pendiente

Se incorporaron los ocho indicadores de `KPIs.docx` al [README](README.md#kpis-aprobados), con las fórmulas, unidades, responsables y fuentes originales. El CSV tiene campos para comenzar a validar los KPI-01 a KPI-07. Si el equipo trabaja con el KPI-08, queda pendiente obtener del catálogo Chinook la relación canción–artista y verificar la unión mediante `IdCancion`.

El CSV contiene 2.240 líneas de factura, 66 columnas, 412 facturas y 59 clientes entre 2009 y 2013. `CategoriaPrecio` tiene 2.129 registros de 0,99 y 111 de 1,99 (aproximadamente 5 %). `PrecioUnitario` coincide con esa etiqueta en todas las filas y `PrecioUnitarioNormalizado` también la distingue de forma exacta. `ImporteLinea` contiene el precio y la cantidad vale 1 en todas las filas.

La propuesta de trabajo es el KPI-04. Permite pasar de un porcentaje que la junta ya conoce a una pregunta sobre cada comprador. La comprobación inicial y el diseño de la entrega se detallan a continuación. Los ocho KPIs conservan su aprobación original. La elección del objetivo predictivo corresponde al equipo.

## Diseño de la entrega final

**Pregunta propuesta.** Al cierre de cada mes, ¿qué clientes que compraron ese mes volverán a comprar durante el mes siguiente? La respuesta permitiría a la junta planificar el seguimiento de compradores recientes. El KPI-04 mide la retención observada del grupo. El modelo estimaría la probabilidad de recompra de cada integrante de ese grupo.

**Qué recibirá la junta.** Un notebook que permita reconstruir el análisis desde el CSV, una comparación de dos modelos con sus errores en casos futuros y una presentación con tres decisiones sustentadas en esos resultados. Para la entrega académica, cada integrante debe poder explicar cómo se construyó un ejemplo, cómo se evaluó una predicción y qué decisión permite tomar la evidencia.

### Evidencia para elegir la pregunta

En el CSV hay ventas en los 60 meses de enero de 2009 a diciembre de 2013. Para examinar el KPI-04, se contaron una sola vez los compradores de cada mes y se comprobó cuáles aparecen también en el mes calendario siguiente. Así se obtienen 59 pares de meses observables. Los 405 casos de la tabla son oportunidades de recompra de 59 clientes, por lo que un mismo cliente puede aportar casos en meses diferentes. Se asignó cada resultado al año del **mes en que se observa la recompra**. [CSV del workshop](data/data_process.csv)

| Año del resultado | Casos cliente-mes | Casos con recompra | Meses de resultado con cero recompras |
| --- | ---: | ---: | ---: |
| 2009, febrero a diciembre | 76 | 11 | 0 |
| 2010 | 83 | 12 | 0 |
| 2011 | 83 | 10 | 2 |
| 2012 | 83 | 0 | 12 |
| 2013 | 80 | 7 | 5 |
| **Total observado** | **405** | **40** | **19** |

Por ejemplo, seis clientes compraron en enero de 2009. Solo el cliente 2 volvió en febrero. El KPI-04 de febrero es 1/6, aproximadamente **16,7 %**. Para modelar, enero aporta seis filas con la misma fecha de corte, una positiva y cinco negativas. La proporción global de positivos, 40/405, pondera por el número de compradores de cada cohorte. Para presentar el KPI aprobado, corresponde mostrar la tasa de **cada mes** con su denominador.

La concentración de los positivos cambia con el tiempo. Una regla que siempre pronostica ausencia de recompra acertaría 365 de los 405 casos históricos (**90,1 %**) y detectaría cero recompras. Además, Chinook documenta que sus ventas son generadas. Estos datos permiten evaluar un método en el caso académico. Para trasladar una acción comercial a clientes reales se necesitarían datos operativos y una medición del efecto de esa acción. [Origen de los datos de Chinook](https://github.com/lerocha/chinook-database#data-sources)

**Cómo encajan los demás indicadores.** KPI-03 aporta el denominador del KPI-04 al tomar los clientes activos del mes anterior. KPI-01, KPI-02 y KPI-05 ayudan a la junta a leer juntos ingresos, gasto por comprador y volumen. KPI-06 y KPI-07 describen la composición del catálogo vendido y la cobertura por país. Para KPI-08 falta enlazar cada canción con su artista y comprobar que la unión conserve las líneas y el total de ingresos. Sus fórmulas y responsables están en el [README](README.md#kpis-aprobados).

Si el equipo prefiere una decisión de planificación financiera, otra pregunta defendible sería pronosticar los ingresos del mes siguiente y traducirlos al crecimiento del KPI-01 usando el ingreso del mes que acaba de cerrar. Habría 60 totales mensuales antes de crear rezagos. Esa opción requeriría regresión, una referencia como el ingreso del último mes y comparación con MAE, RMSE y R². El plan que sigue desarrolla la opción de retención. [Métodos de referencia para pronósticos, Hyndman y Athanasopoulos](https://otexts.com/fpp3/simple-methods.html)

### Parte 1 · Pregunta, EDA y datos para el modelo

**Brian lidera y Miguel comprueba la etiqueta.** Esta parte ocupa las primeras secciones del notebook después de la introducción.

1. **Planteamiento.** Identificar al usuario de la predicción, la decisión que tomará y el momento en que recibe el resultado. Definir la clase positiva como «compró al menos una vez en el mes siguiente». Explicar con el ejemplo de enero y febrero cómo se pasa de línea de factura a cliente-mes y de cliente-mes a tasa mensual.
2. **Calidad del CSV.** Presentar dimensiones, tipos, cardinalidad, rango de fechas y nulos por campo. Verificar que cada identificador de línea sea único y que las varias líneas de una misma factura se conserven. Contrastar importe con precio por cantidad y revisar los meses de cobertura. La última venta registrada es del 22 de diciembre de 2013. El CSV concilia con las exportaciones originales del Lab 4 y se adopta diciembre como mes de resultado del historial cerrado de la práctica.
3. **Exploración.** Graficar por mes el número de compradores, las recompras y la tasa. Acompañar los porcentajes con los conteos. Usar boxplots e IQR para revisar gasto y frecuencia por cliente en entrenamiento. Una compra grande válida sigue siendo evidencia comercial. Registrar qué valores se conservaron, corrigieron o imputaron y por qué. Examinar correlaciones entre gasto, unidades y número de facturas antes de elegir predictores.
4. **Tabla para entrenar.** Una fila por comprador activo y por mes de corte. Proponer como predictores los días desde la última compra al cierre, el número de facturas distintas, el gasto acumulado y la diversidad de géneros del periodo observado. Documentar la ventana histórica para cada uno y el tratamiento de clientes con poca historia al inicio del extracto. Usar el identificador para agrupar y comprobar las filas. Reservar toda la actividad del mes siguiente exclusivamente para construir la etiqueta. Diciembre de 2013 como **mes de corte** carece de enero de 2014 para observar el desenlace.

**Entrega a Jeremy.** Diccionario breve con nombre, unidad, ventana temporal y función de cada campo, conteos por mes y un ejemplo rastreable al CSV. El equipo podrá pasar al modelado cuando reconstruya la etiqueta de un cliente a mano y pueda explicar qué conocía al emitir la predicción.

**Implementación de la Fase I, 23 de noviembre.** El notebook construye `resultados/tablas/cliente_mes.csv` y su diccionario. Usa ventanas de 90 días para frecuencia, gasto y diversidad, y calcula recencia, antigüedad observada, cobertura del historial y país conocido al corte. Los controles verifican etiquetas por un cálculo independiente y reconstruyen tres cortes después de retirar ventas futuras. En el bloque inicial de 2009, gasto y unidades tienen correlación 1. Se propone usar gasto y conservar unidades para auditoría. El IQR marca casos válidos de frecuencia, diversidad y cobertura inicial. Se conservan los registros.

**Cobertura adoptada.** `ULTIMO_MES_RESULTADO_COMPLETO` vale `2013-12`. Se verificó que todas las líneas del CSV procesado coinciden con `InvoiceLine.csv` unido a `Invoice.csv` del Lab 4 en claves, cliente, fecha, contenido, cantidad, precio e importe. Los totales por factura también coinciden. Diciembre tiene 38 líneas en siete facturas, con siete compradores y 38,62 UM, consistentes con la línea base del Proyecto II. Se adopta el conjunto cerrado de la práctica con 405 casos y 40 positivos, de los cuales 325 son anteriores a 2013 y 80 corresponden a 2013. El último corte es noviembre y su etiqueta se observa en diciembre.

**Verificación local.** En el cierre inicial se ejecutaron las 13 celdas de código de la Fase I con Matplotlib 3.11.2, se exportaron seis tablas y cuatro figuras y se revisaron visualmente. Al incorporar diciembre se recalcularon las diez celdas de datos y se conciliaron 59 tasas mensuales de retención con el Proyecto II. Los 398 casos previos conservan sus valores y se agregan siete casos con una recompra. Los datos que alimentan las gráficas de desarrollo y el EDA inicial de 2009 son idénticos a los de la ejecución anterior. Se conservan sus salidas e imágenes revisadas. La ejecución completa del proyecto se comprobará nuevamente cuando estén implementadas las fases de los demás integrantes.

### Parte 2 · Diseño de la prueba y entrenamiento

**Jeremy lidera y Brian revisa las fechas.** Registrar el protocolo antes de comparar resultados. La propuesta reserva los desenlaces de enero a diciembre de 2013 para prueba y usa los anteriores para desarrollo. La tabla de la Fase I contiene 80 casos con resultado en 2013 y siete positivos. Mantener reservadas para el final las predicciones y métricas de 2013.

| Elemento | Cómo debe quedar explicado en el notebook |
| --- | --- |
| Partición | Indicar fechas de corte y meses de resultado. Para predecir enero de 2013 se usan los compradores y la información disponible al cierre de diciembre de 2012. Mantener cada mes completo dentro del mismo bloque. Es válido reconocer a un cliente que vuelve a aparecer porque el uso previsto es puntuar compradores conocidos en fechas futuras. |
| Validación | Dentro del desarrollo, entrenar con el pasado y evaluar bloques posteriores. Por ejemplo, entrenar hasta los desenlaces de 2009 y validar 2010, ampliar hasta 2010 y validar 2011, y ampliar hasta 2011 y validar 2012. Conservar el bloque de 2012 para medir falsas alarmas. ROC/AUC queda indefinida en un bloque de una sola clase. Anotar esa condición al lado de los conteos. |
| Preparación | Aprender imputación, escalado y codificación sobre el entrenamiento de cada bloque. Escalar variables numéricas para la regresión logística. Si se incluye país, gestionar categorías nuevas. Registrar semilla para operaciones aleatorias y explicar la decisión de preservar el orden cronológico ante el desbalance. |
| Referencia | Predecir siempre la clase más frecuente y usar la proporción de recompras del entrenamiento como puntuación constante. Presentar esta referencia junto a los dos modelos. |
| Modelo 1 | Regresión logística regularizada. Probar unas pocas intensidades de regularización y explicar cómo limitan coeficientes extremos con pocos positivos. |
| Modelo 2 | Árbol de decisión de profundidad limitada. Comparar profundidades y tamaños mínimos de hoja que permitan comprobar si hay reglas sencillas de frecuencia y recencia. Documentar los candidatos y el ajuste elegido. |
| Selección | Proponer **F1 de la clase recompra** como criterio inicial si precisión y cobertura importan por igual. Elegir configuración y umbral con las predicciones de validación temporal, reuniendo los conteos de los bloques y mostrando también el desglose anual. Si la junta prioriza otro coste, acordar el criterio antes de mirar el desempeño final. |

**Entrega a Miguel.** Dos modelos ajustados sobre desarrollo, con variables, parámetros, umbrales, fechas y criterio de selección registrados. El mismo preprocesamiento debe poder aplicarse a cada mes futuro con información disponible en su cierre. [Validación temporal con origen móvil](https://otexts.com/fpp3/tscv.html) · [Prevención de fuga de información](https://scikit-learn.org/stable/common_pitfalls.html#data-leakage) · [Elección del umbral de decisión](https://scikit-learn.org/stable/modules/classification_threshold.html)

### Parte 3 · Comparación, errores e interpretación

**Miguel lidera y Jeremy reproduce la comparación.** Aplicar los modelos fijados a los mismos casos reservados. Elaborar una tabla con una fila para la referencia y una para cada modelo. Incluir tamaño de prueba, positivos reales, umbral, exactitud, ROC/AUC, precisión, recall y F1. Trazar las curvas ROC usando las puntuaciones de los modelos. Adjuntar matrices de confusión con ejes y clase positiva identificados. Conservar las predicciones al nivel cliente-mes para rastrear de dónde sale cada cifra. [Métricas de evaluación de scikit-learn](https://scikit-learn.org/stable/modules/model_evaluation.html)

Explicar qué sucede cuando el modelo anticipa una recompra que no ocurre y cuando pasa por alto una recompra real. Hay siete positivos en los resultados de 2013. Acertar o perder **un solo caso** mueve el recall unos 14,3 puntos porcentuales. Mostrar los conteos junto a los porcentajes y señalar si la utilidad se concentra en pocos meses. Sustentar la selección comparando desempeño, facilidad de interpretación y estabilidad. Si la referencia sigue siendo competitiva, ese es un resultado defendible para la junta.

Para interpretar el modelo elegido, mostrar cuánto cambia una métrica al permutar una variable en datos de validación con ambas clases. Revisar las variables correlacionadas y explicar con un ejemplo cómo leyó el modelo una característica del historial. Una asociación predictiva puede orientar una hipótesis comercial. Para afirmar que una intervención incrementa la recompra se necesitaría medir su efecto. [Importancia por permutación y predictores correlacionados](https://scikit-learn.org/stable/modules/permutation_importance.html)

**Entrega a Cristopher.** Una tabla comparativa en `resultados/tablas/`, las figuras de evaluación e importancia en `resultados/figuras/` y una conclusión que identifique el modelo preferido, su principal error y las condiciones de uso.

### Parte 4 · Decisiones de negocio y defensa

**Cristopher lidera y los cuatro defienden.** Cada recomendación final debe identificar quién decide, qué acción se tomaría, qué resultado del modelo la justifica y cómo se medirá después. Estas tres decisiones quedan condicionadas a los resultados:

| Decisión para la junta | Evidencia que debe presentar el equipo | Seguimiento propuesto |
| --- | --- | --- |
| Probar una comunicación de novedades con un grupo de compradores recientes | El modelo concentra recompras futuras en el grupo priorizado mejor que la referencia y en un volumen atendible. | Comparar grupos equivalentes asignados al azar a recibir o no el contacto. Medir KPI-04 y coste por recompra adicional. |
| Fijar cuántos clientes puede atender el equipo comercial por mes | Mostrar cómo cambian los contactos, los aciertos y las falsas alarmas con umbrales comparados en validación. | Revisar mensualmente cupo, coste de contacto y compras observadas en la cohorte. |
| Decidir en qué condiciones mantener o suspender la priorización automática | Documentar si la ventaja se sostiene en periodos diferentes y qué ocurre en meses sin recompras. | Revisar errores y volumen de positivos al cierre. Si la ventaja es insuficiente, mantener una regla sencilla y recoger más meses antes de ampliar el uso. |

**Guion propuesto de 12 láminas y 20 minutos.** Brian dedica cinco minutos a la decisión de la junta, el KPI y la construcción de la etiqueta (láminas 1–3). Jeremy explica con una línea de tiempo la partición, la referencia y los dos modelos (4–6, cinco minutos). Miguel presenta las métricas comparativas, los errores en clientes y las variables relevantes (7–9, cinco minutos). Cristopher cierra con las decisiones, las limitaciones y cómo se medirá el resultado del piloto (10–12, cinco minutos). Los cinco minutos siguientes son para preguntas individuales.

En el ensayo, cada integrante explica una decisión de otra fase. Preguntas útiles son «¿por qué 2.240 líneas se convierten en 405 casos?», «¿qué información habría sido futura al cierre de enero?», «¿qué sucede con ROC/AUC en 2012?» y «¿cómo distinguiríamos una recompra prevista de una compra adicional causada por la campaña?». Registrar en el histórico los aportes y revisiones de cada persona.

### Comprobación de la entrega completa

| Evidencia al cierre | Ubicación y criterio de aceptación |
| --- | --- |
| Notebook reproducible | `notebooks/proyecto_3.ipynb`. Desde un kernel limpio, el equipo carga el CSV con ruta relativa y ejecuta todas las celdas en orden. El Markdown identifica el objetivo final, las decisiones y las conclusiones. Indicar versiones usadas, semilla y fechas de corte. |
| Resultados rastreables | `resultados/tablas/` y `resultados/figuras/`. Los totales de las matrices coinciden con los casos de prueba. Las cifras, unidades y etiquetas de las diapositivas coinciden con las salidas del notebook. |
| Presentación lista para la junta | `presentacion/`. Incluir decisión de negocio, comparación, variables relevantes, tres recomendaciones y límites de aplicación. Ensayar los 20 minutos con los cuatro integrantes. |
| Cierre del equipo | Actualizar el README con la pregunta elegida y las instrucciones reales de ejecución. Registrar en esta bitácora aportes, revisiones y pendientes resueltos. |

El enunciado del proyecto, en sus fases I a IV y rúbrica, define los requisitos de evaluación resumidos abajo. El reparto, el calendario de prueba y las acciones comerciales de esta guía son propuestas del equipo de trabajo para cumplirlos. El modelo ganador, sus métricas y las recomendaciones definitivas se completarán con el trabajo experimental.

## Entregables y criterios de cierre

- **Notebook reproducible.** Usar pandas, NumPy, Matplotlib o Seaborn y scikit-learn. Documentar en Markdown el objetivo, EDA, limpieza, ingeniería de variables, partición, modelos y conclusiones. Fijar la semilla, estratificar si hay desbalance según el enunciado y ajustar las transformaciones y los hiperparámetros con entrenamiento. La aceptación de la partición cronológica está pendiente de confirmación.
- **Comparación sobre prueba independiente.** En clasificación, incluir matriz de confusión, exactitud y curva ROC/AUC. Si hay desbalance, añadir precisión, recall y F1 para interpretar la clase minoritaria. En regresión, incluir RMSE, MAE y R². Justificar el modelo elegido y mostrar la importancia de sus variables.
- **Presentación ejecutiva.** Apuntar a 12 láminas dentro del límite indicado de 12 a 15. Explicar el impacto de las métricas para Grupo Innova S.A. y sustentar tres decisiones concretas. Ensayar 20 minutos de exposición y 5 de preguntas técnicas individuales.
- **Rúbrica completa compartida el 23 de noviembre.** EDA y preparación 10 %, modelado y entrenamiento 30 %, evaluación y selección 20 %, impacto y recomendaciones 10 %, defensa oral y dominio individual 30 %. La defensa dura 20 minutos de exposición y 5 de preguntas individuales. El enunciado también evalúa la participación individual y la colaboración con el equipo. En el reparto vigente, Jeremy implementa la codificación, el escalado y la partición dentro de su flujo de entrenamiento. Esos requisitos completan la Fase I del enunciado junto con el EDA y la ingeniería de variables de Brian.


### Implementación de la Fase II de Jeremy · 24 de noviembre

Se continúa con el objetivo de recompra construido por Brian. Desarrollo
contiene 325 casos anteriores a 2013; los 80 casos con resultado en 2013 quedan
reservados para la Fase III de Miguel. La ratificación de la pregunta por todo
el equipo conserva su estado pendiente.

Los tres bloques crecientes entrenan hasta 2009/2010/2011 y validan
2010/2011/2012. Se mantienen los meses completos. La partición aleatoria
estratificada se sustituye por una validación cronológica coherente con el
momento de predicción, documentando el desbalance y comparando pesos de clase.

Se ajustan ocho configuraciones de regresión logística y doce de árbol,
con nueve umbrales fijados previamente. Los transformadores se aprenden
dentro del entrenamiento de cada bloque. El criterio es F1 positivo conjunto
de las 249 predicciones fuera de entrenamiento. Se registra también el
desglose anual y se conserva 2012 con ROC/AUC no definida por tener una clase.

La logística quedó con C=1 y umbral 0.1; el árbol, con profundidad 2, diez
casos por hoja y umbral 0.5. Ambos quedaron sin pesos. Sus F1 de validación
son 0.3048 y 0.5484. Los dos pipelines finales y la referencia se ajustan con
desarrollo; sus resultados de prueba y el ganador quedan para Miguel.

El notebook deja `modelos_ajustados`, `umbrales_modelos`, `X_prueba`,
`y_prueba`, las claves reservadas y modelos por bloque para continuar la
interpretación con validación fuera de entrenamiento. Exporta ocho archivos
de tablas/protocolo y dos figuras `fase2_*`. La Fase I y el CSV de entrada
conservan sus datos. La ejecución de las fases implementadas pasó desde un
kernel nuevo con 21 celdas de código, incluida la celda de instalación de
Matplotlib que ya existía.

## Histórico

| Fecha | Responsable | Avance verificado | Siguiente paso |
| --- | --- | --- | --- |
| 2026-11-21 | Preparación del repositorio | Enunciado revisado, CSV inspeccionado con Python y estructura inicial creada. Se detectaron columnas que revelan `CategoriaPrecio`. | Reunir al equipo para definir el objetivo y el protocolo de validación. |
| 2026-11-21 | Organización de datos | CSV movido a `data/` y ruta de carga documentada. Se verificó que el contenido del archivo se conservó. | Usar el CSV de `data/` al crear el notebook. |
| 2026-11-21 | Estructura del proyecto | Se organizaron los datos de entrada y derivados, los borradores, el notebook final, las exportaciones y la defensa. Se documentaron las rutas en el README. | Registrar los KPIs aprobados y usar `data/entrada/data_process.csv` para iniciar el análisis. |
| 2026-11-21 | Simplificación de carpetas | El CSV quedó directamente en `data/` y los notebooks directamente en `notebooks/`. En `resultados/` se mantienen carpetas para figuras y tablas. | Registrar los KPIs aprobados y usar `data/data_process.csv` para iniciar el análisis. |
| 2026-11-21 | Incorporación de KPIs | Se documentaron los ocho KPIs del Word, se revisaron las columnas del CSV y se redactó la introducción del notebook. | Acordar el KPI prioritario y comprobar la viabilidad de la pregunta predictiva. |
| 2026-11-21 | Investigación y diseño | Se contrastaron rúbrica, KPIs, CSV y fuentes metodológicas. Se documentaron 405 casos observables y 40 recompras, las cuatro fases, los productos de cada integrante y el guion de defensa. | Acordar el objetivo y verificar la cobertura al cierre de diciembre de 2013 antes de construir el conjunto de modelado. |
| 2026-11-23 | Fase I de Brian | Intercambio de fases con Miguel registrado. Se revisaron el KPI-04 del Proyecto II y la organización de los scripts de R. Se implementaron el EDA, la etiqueta, 398 ejemplos cliente-mes, seis tablas derivadas y el diccionario. Cálculos y controles temporales ejecutados. Gráficas pendientes de Matplotlib. | Ejecutar las gráficas en Colab, ratificar la pregunta y confirmar cobertura de diciembre. Miguel continúa con partición y modelos. |
| 2026-11-23 | Organización de commits de Brian | Fase I organizada en cinco avances. Carga y calidad en `114d6a0`, construcción de casos en `47f68b7`, análisis de variables en `d980d5c` y validación y exportaciones en `241f98a`. El quinto avance incorpora las instrucciones y el reparto actualizado. | Ejecutar las gráficas en Colab y revisar la entrega con Miguel. |
| 2026-11-23 | Cierre del EDA de Brian | Dependencias oficiales obtenidas desde PyPI. Se ejecutaron las 13 celdas de código de la Fase I, se revisaron cuatro figuras y se añadieron conclusiones y puntos de defensa. Se comprobó la rúbrica completa, incluido el 30 % de defensa. El quinto commit incorpora este cierre. | Ratificar la pregunta de recompra y confirmar la cobertura de diciembre. Miguel continúa con partición, preprocesamiento y modelos. |
| 2026-11-23 | Inclusión de diciembre por Brian | CSV conciliado con las exportaciones originales del Lab 4. Se adopta diciembre como mes de resultado, se agregan siete casos y una recompra y se concilian 59 tasas mensuales con el Proyecto II. Las tablas y explicaciones se actualizan a 405 casos y 40 recompras. | Miguel recibe 325 casos anteriores a 2013 y 80 casos de 2013 para registrar su protocolo temporal. El equipo ratifica la pregunta de recompra. |
| 2026-11-23 | Guía de ejecución para el equipo | README ampliado con selección del kernel, extensiones Python y Jupyter, instalación de dependencias por entorno y ejecución mediante Restart y Run All. Se documentaron los errores de biblioteca ausente y variable sin definir observados durante la ejecución de Brian. | Cada integrante prepara su entorno y ejecuta el notebook desde el principio antes de continuar su fase. |
| 2026-11-24 | Fase II de Jeremy | Intercambio con Miguel registrado en el reparto vigente. Partición temporal, pipelines, referencia y dos algoritmos ajustados con validación 2010–2012; 2013 reservado. Se ejecutaron las 21 celdas de código de las fases I y II y se generaron dos figuras y ocho archivos de control/validación. | Miguel continúa la Fase III: comparación en prueba, errores e importancia. Cristopher prepara la interpretación ejecutiva. |
| 2026-11-27 | Revisión del proyecto | Se contrastaron los commits, el PDF y los archivos de salida. Se identificaron la comprobación de estratificación pendiente, las discrepancias de ejecución y la ausencia de resultados finales de prueba y presentación. | Confirmar el protocolo y completar la evaluación de 2013. |
| 2026-11-28 | Fase III · Miguel | Se completaron y reprodujeron la comparación de 2013, las figuras, las exportaciones, la selección de la regresión logística y su interpretación por permutación. | Entregar los resultados a Cristopher para la Fase IV y preparar la defensa del equipo. |

Durante el trabajo de Brian se corrigió el correo de autor y committer de cinco commits para usar su dirección privada de GitHub después del rechazo GH007.

En cada sesión, agregar una fila con fecha, participantes, avance comprobable, enlace al archivo o commit si existe y siguiente paso. Actualizar el estado y los resultados cuando el avance se pueda verificar. Registrar aquí las decisiones que cambien el objetivo, los datos o la evaluación y por qué se tomaron.
