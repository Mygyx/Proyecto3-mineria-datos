# Bitácora del Proyecto III de Minería de Datos

Curso ISW-911 · Caso Grupo Innova S.A. · Python y Jupyter Notebook

Equipo: Miguel, Brian, Jeremy y Crisphofer.

## Estado actual

- [x] Leer el enunciado y resumir los requisitos de entrega y defensa.
- [x] Confirmar que el repositorio tiene el CSV procesado del workshop 4 y revisar su estructura inicial.
- [x] Crear las carpetas y registrar un reparto propuesto.
- [x] Registrar los ocho KPIs aprobados por el profesor y revisar los campos disponibles en el CSV.
- [x] Redactar la introducción del notebook con el contexto de Chinook y los KPIs.
- [x] Investigar una ruta de clasificación vinculada al KPI-04, comprobar las etiquetas observables en el CSV y diseñar las cuatro fases de la entrega.
- [ ] Acordar la pregunta de negocio, la unidad de análisis y la variable objetivo.
- [ ] Completar el EDA y definir el preprocesamiento y la partición.
- [ ] Entrenar y ajustar al menos dos modelos supervisados.
- [ ] Evaluar ambos modelos en prueba independiente, seleccionar uno y explicar sus variables más importantes.
- [ ] Ejecutar el notebook completo y preparar y ensayar la defensa.

## Estructura del repositorio

| Ruta | Uso |
| --- | --- |
| [README.md](README.md) | Estructura del repositorio y rutas de carga según el directorio de trabajo. |
| [data/](data/) | Contiene [data_process.csv](data/data_process.csv), el insumo procesado del workshop 4. |
| [proyecto_3.ipynb](notebooks/proyecto_3.ipynb) | Notebook de entrega. Introducción redactada. Análisis y modelado pendientes. |
| [resultados/figuras/](resultados/figuras/) | Gráficos exportados para comparación y defensa. |
| [resultados/tablas/](resultados/tablas/) | Tablas exportadas, incluida la comparación sobre el conjunto de prueba. |
| [presentacion/](presentacion/) | Diapositivas ejecutivas y material de ensayo. |
| [agentes.md](agentes.md) | Estado, decisiones y aportes del equipo. |

## Reparto propuesto

| Responsable | Trabajo principal | Entrega al equipo |
| --- | --- | --- |
| Miguel | Fase I. Plantear la pregunta de negocio, justificar el objetivo, hacer EDA y definir qué variables están disponibles al predecir. | Unidad de análisis, objetivo y predictores aprobados por el equipo. Diagnóstico de tipos, cardinalidad, faltantes, atípicos y correlaciones. |
| Brian | Fase II. Implementar la partición y el preprocesamiento reproducible. Entrenar y ajustar al menos dos algoritmos adecuados usando validación dentro de entrenamiento. | Modelos comparables, hiperparámetros justificados y flujo reproducible de codificación, escalado e imputación según corresponda. |
| Jeremy | Fase III. Evaluar ambos modelos sobre la misma prueba independiente y justificar la selección. Analizar los errores y estimar la importancia de las variables del modelo elegido. | Tabla de métricas, figuras e interpretación técnica para la presentación. |
| Crisphofer | Fase IV. Convertir las métricas y la importancia de variables en conclusiones de negocio. Preparar las diapositivas y coordinar el ensayo. | Presentación con impacto operativo y al menos tres decisiones estratégicas concretas derivadas de los resultados. |

Los cuatro acuerdan el objetivo y el esquema de validación antes de modelar. Cada integrante revisa el notebook completo y practica explicar el código, la teoría y las decisiones de las cuatro fases.

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

**Miguel lidera y Jeremy comprueba la etiqueta.** Esta parte ocupa las primeras secciones del notebook después de la introducción.

1. **Planteamiento.** Identificar al usuario de la predicción, la decisión que tomará y el momento en que recibe el resultado. Definir la clase positiva como «compró al menos una vez en el mes siguiente». Explicar con el ejemplo de enero y febrero cómo se pasa de línea de factura a cliente-mes y de cliente-mes a tasa mensual.
2. **Calidad del CSV.** Presentar dimensiones, tipos, cardinalidad, rango de fechas y nulos por campo. Verificar que cada identificador de línea sea único y que las varias líneas de una misma factura se conserven. Contrastar importe con precio por cantidad y revisar los meses de cobertura. La última venta registrada es del 22 de diciembre de 2013. Confirmar en el workshop si el extracto cubre el cierre mensual antes de tratar diciembre como mes de resultado completo.
3. **Exploración.** Graficar por mes el número de compradores, las recompras y la tasa. Acompañar los porcentajes con los conteos. Usar boxplots e IQR para revisar gasto y frecuencia por cliente en entrenamiento. Una compra grande válida sigue siendo evidencia comercial. Registrar qué valores se conservaron, corrigieron o imputaron y por qué. Examinar correlaciones entre gasto, unidades y número de facturas antes de elegir predictores.
4. **Tabla para entrenar.** Una fila por comprador activo y por mes de corte. Proponer como predictores los días desde la última compra al cierre, el número de facturas distintas, el gasto acumulado y la diversidad de géneros del periodo observado. Documentar la ventana histórica para cada uno y el tratamiento de clientes con poca historia al inicio del extracto. Usar el identificador para agrupar y comprobar las filas. Reservar toda la actividad del mes siguiente exclusivamente para construir la etiqueta. Diciembre de 2013 como **mes de corte** carece de enero de 2014 para observar el desenlace.

**Entrega a Brian.** Diccionario breve con nombre, unidad, ventana temporal y función de cada campo, conteos por mes y un ejemplo rastreable al CSV. El equipo podrá pasar al modelado cuando reconstruya la etiqueta de un cliente a mano y pueda explicar qué conocía al emitir la predicción.

### Parte 2 · Diseño de la prueba y entrenamiento

**Brian lidera y Miguel revisa las fechas.** Registrar el protocolo antes de comparar resultados. La propuesta reserva los desenlaces de 2013 para prueba y usa los anteriores para desarrollo. La comprobación de viabilidad anterior ya mostró la composición por año. Mantener reservadas para el final las predicciones y métricas de 2013. Si se confirma que diciembre está incompleto, documentar el motivo y cerrar la prueba en noviembre.

| Elemento | Cómo debe quedar explicado en el notebook |
| --- | --- |
| Partición | Indicar fechas de corte y meses de resultado. Para predecir enero de 2013 se usan los compradores y la información disponible al cierre de diciembre de 2012. Mantener cada mes completo dentro del mismo bloque. Es válido reconocer a un cliente que vuelve a aparecer porque el uso previsto es puntuar compradores conocidos en fechas futuras. |
| Validación | Dentro del desarrollo, entrenar con el pasado y evaluar bloques posteriores. Por ejemplo, entrenar hasta los desenlaces de 2009 y validar 2010, ampliar hasta 2010 y validar 2011, y ampliar hasta 2011 y validar 2012. Conservar el bloque de 2012 para medir falsas alarmas. ROC/AUC queda indefinida en un bloque de una sola clase. Anotar esa condición al lado de los conteos. |
| Preparación | Aprender imputación, escalado y codificación sobre el entrenamiento de cada bloque. Escalar variables numéricas para la regresión logística. Si se incluye país, gestionar categorías nuevas. Registrar semilla para operaciones aleatorias y explicar la decisión de preservar el orden cronológico ante el desbalance. |
| Referencia | Predecir siempre la clase más frecuente y usar la proporción de recompras del entrenamiento como puntuación constante. Presentar esta referencia junto a los dos modelos. |
| Modelo 1 | Regresión logística regularizada. Probar unas pocas intensidades de regularización y explicar cómo limitan coeficientes extremos con pocos positivos. |
| Modelo 2 | Árbol de decisión de profundidad limitada. Comparar profundidades y tamaños mínimos de hoja que permitan comprobar si hay reglas sencillas de frecuencia y recencia. Documentar los candidatos y el ajuste elegido. |
| Selección | Proponer **F1 de la clase recompra** como criterio inicial si precisión y cobertura importan por igual. Elegir configuración y umbral con las predicciones de validación temporal, reuniendo los conteos de los bloques y mostrando también el desglose anual. Si la junta prioriza otro coste, acordar el criterio antes de mirar el desempeño final. |

**Entrega a Jeremy.** Dos modelos ajustados sobre desarrollo, con variables, parámetros, umbrales, fechas y criterio de selección registrados. El mismo preprocesamiento debe poder aplicarse a cada mes futuro con información disponible en su cierre. [Validación temporal con origen móvil](https://otexts.com/fpp3/tscv.html) · [Prevención de fuga de información](https://scikit-learn.org/stable/common_pitfalls.html#data-leakage) · [Elección del umbral de decisión](https://scikit-learn.org/stable/modules/classification_threshold.html)

### Parte 3 · Comparación, errores e interpretación

**Jeremy lidera y Brian reproduce la comparación.** Aplicar los modelos fijados a los mismos casos reservados. Elaborar una tabla con una fila para la referencia y una para cada modelo. Incluir tamaño de prueba, positivos reales, umbral, exactitud, ROC/AUC, precisión, recall y F1. Trazar las curvas ROC usando las puntuaciones de los modelos. Adjuntar matrices de confusión con ejes y clase positiva identificados. Conservar las predicciones al nivel cliente-mes para rastrear de dónde sale cada cifra. [Métricas de evaluación de scikit-learn](https://scikit-learn.org/stable/modules/model_evaluation.html)

Explicar qué sucede cuando el modelo anticipa una recompra que no ocurre y cuando pasa por alto una recompra real. Si se mantienen los siete positivos observados en el año de prueba, acertar o perder **un solo caso** mueve el recall unos 14,3 puntos porcentuales. Mostrar los conteos junto a los porcentajes y señalar si la utilidad se concentra en pocos meses. Sustentar la selección comparando desempeño, facilidad de interpretación y estabilidad. Si la referencia sigue siendo competitiva, ese es un resultado defendible para la junta.

Para interpretar el modelo elegido, mostrar cuánto cambia una métrica al permutar una variable en datos de validación con ambas clases. Revisar las variables correlacionadas y explicar con un ejemplo cómo leyó el modelo una característica del historial. Una asociación predictiva puede orientar una hipótesis comercial. Para afirmar que una intervención incrementa la recompra se necesitaría medir su efecto. [Importancia por permutación y predictores correlacionados](https://scikit-learn.org/stable/modules/permutation_importance.html)

**Entrega a Crisphofer.** Una tabla comparativa en `resultados/tablas/`, las figuras de evaluación e importancia en `resultados/figuras/` y una conclusión que identifique el modelo preferido, su principal error y las condiciones de uso.

### Parte 4 · Decisiones de negocio y defensa

**Crisphofer lidera y los cuatro defienden.** Cada recomendación final debe identificar quién decide, qué acción se tomaría, qué resultado del modelo la justifica y cómo se medirá después. Estas tres decisiones quedan condicionadas a los resultados:

| Decisión para la junta | Evidencia que debe presentar el equipo | Seguimiento propuesto |
| --- | --- | --- |
| Probar una comunicación de novedades con un grupo de compradores recientes | El modelo concentra recompras futuras en el grupo priorizado mejor que la referencia y en un volumen atendible. | Comparar grupos equivalentes asignados al azar a recibir o no el contacto. Medir KPI-04 y coste por recompra adicional. |
| Fijar cuántos clientes puede atender el equipo comercial por mes | Mostrar cómo cambian los contactos, los aciertos y las falsas alarmas con umbrales comparados en validación. | Revisar mensualmente cupo, coste de contacto y compras observadas en la cohorte. |
| Decidir en qué condiciones mantener o suspender la priorización automática | Documentar si la ventaja se sostiene en periodos diferentes y qué ocurre en meses sin recompras. | Revisar errores y volumen de positivos al cierre. Si la ventaja es insuficiente, mantener una regla sencilla y recoger más meses antes de ampliar el uso. |

**Guion propuesto de 12 láminas y 20 minutos.** Miguel dedica cinco minutos a la decisión de la junta, el KPI y la construcción de la etiqueta (láminas 1–3). Brian explica con una línea de tiempo la partición, la referencia y los dos modelos (4–6, cinco minutos). Jeremy presenta las métricas comparativas, los errores en clientes y las variables relevantes (7–9, cinco minutos). Crisphofer cierra con las decisiones, las limitaciones y cómo se medirá el resultado del piloto (10–12, cinco minutos). Los cinco minutos siguientes son para preguntas individuales.

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

- **Notebook reproducible.** Usar pandas, NumPy, Matplotlib o Seaborn y scikit-learn. Documentar en Markdown el objetivo, EDA, limpieza, ingeniería de variables, partición, modelos y conclusiones. Fijar la semilla cuando corresponda, estratificar si hay desbalance y el esquema lo permite, y ajustar las transformaciones y los hiperparámetros con entrenamiento.
- **Comparación sobre prueba independiente.** En clasificación, incluir matriz de confusión, exactitud y curva ROC/AUC. Si hay desbalance, añadir precisión, recall y F1 para interpretar la clase minoritaria. En regresión, incluir RMSE, MAE y R². Justificar el modelo elegido y mostrar la importancia de sus variables.
- **Presentación ejecutiva.** Apuntar a 12 láminas dentro del límite indicado de 12 a 15. Explicar el impacto de las métricas para Grupo Innova S.A. y sustentar tres decisiones concretas. Ensayar 20 minutos de exposición y 5 de preguntas técnicas individuales.
- **Rúbrica.** EDA y preparación 10 %, modelado y entrenamiento 30 %, evaluación y selección 20 %, impacto y recomendaciones 10 %, defensa y dominio individual 30 %. El enunciado también contempla la participación individual.

## Histórico

| Fecha | Responsable | Avance verificado | Siguiente paso |
| --- | --- | --- | --- |
| 2026-11-21 | Preparación del repositorio | Enunciado revisado, CSV inspeccionado con Python y estructura inicial creada. Se detectaron columnas que revelan `CategoriaPrecio`. | Reunir al equipo para definir el objetivo y el protocolo de validación. |
| 2026-11-21 | Organización de datos | CSV movido a `data/` y ruta de carga documentada. Se verificó que el contenido del archivo se conservó. | Usar el CSV de `data/` al crear el notebook. |
| 2026-11-21 | Estructura del proyecto | Se organizaron los datos de entrada y derivados, los borradores, el notebook final, las exportaciones y la defensa. Se documentaron las rutas en el README. | Registrar los KPIs aprobados y usar `data/entrada/data_process.csv` para iniciar el análisis. |
| 2026-11-21 | Simplificación de carpetas | El CSV quedó directamente en `data/` y los notebooks directamente en `notebooks/`. En `resultados/` se mantienen carpetas para figuras y tablas. | Registrar los KPIs aprobados y usar `data/data_process.csv` para iniciar el análisis. |
| 2026-11-21 | Incorporación de KPIs | Se documentaron los ocho KPIs del Word, se revisaron las columnas del CSV y se redactó la introducción del notebook. | Acordar el KPI prioritario y comprobar la viabilidad de la pregunta predictiva. |
| 2026-11-21 | Investigación y diseño | Se contrastaron rúbrica, KPIs, CSV y fuentes metodológicas. Se documentaron 405 casos observables y 40 recompras, las cuatro fases, los productos de cada integrante y el guion de defensa. | Acordar el objetivo y verificar la cobertura al cierre de diciembre de 2013 antes de construir el conjunto de modelado. |

En cada sesión, agregar una fila con fecha, participantes, avance comprobable, enlace al archivo o commit si existe y siguiente paso. Actualizar las casillas cuando el avance se pueda verificar. Registrar aquí las decisiones que cambien el objetivo, los datos o la evaluación y por qué se tomaron.
