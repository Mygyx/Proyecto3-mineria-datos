# Proyecto3-mineria-datos

Proyecto III de ISW-911. El equipo entregará un notebook reproducible en Python y una presentación ejecutiva para el caso Grupo Innova S.A.

## Estructura del repositorio

```text
Proyecto3-mineria-datos/
├── data/
│   └── data_process.csv
├── notebooks/
├── resultados/
│   ├── figuras/
│   └── tablas/
├── presentacion/
├── agentes.md
└── README.md
```

- `data/` contiene el CSV recibido del workshop 4.
- `notebooks/proyecto_3.ipynb` contiene la introducción y la Fase I de Brian, con el EDA y la construcción de la tabla cliente-mes, y la Fase II de Jeremy, con partición y entrenamiento. Miguel y Cristopher incorporarán las fases III y IV al mismo notebook. Antes de entregar, debe poder ejecutarse de principio a fin usando el CSV de entrada.
- `resultados/figuras/` y `resultados/tablas/` reúnen las exportaciones del notebook, como gráficos de evaluación, importancia de variables y la comparación de modelos en prueba.
- `presentacion/` guarda las diapositivas y el guion de defensa. La presentación utiliza los resultados exportados desde el notebook.
- `agentes.md` registra localmente las decisiones, las tareas y el avance de cada integrante.

La ruta del CSV depende del directorio de trabajo de Jupyter.

| Directorio de trabajo | Ruta para `pd.read_csv()` |
| --- | --- |
| Raíz del repositorio | `data/data_process.csv` |
| `notebooks/` | `../data/data_process.csv` |

## KPIs aprobados

Los ocho indicadores provienen de `KPIs.docx`, preparado para el Proyecto 2 con el Data Warehouse Chinook del Proyecto 1. Todos se miden mensualmente. Los responsables se reproducen como aparecen en el documento. Las metas se definirán después de calcular las líneas base históricas.

| Código e indicador | Responsable | Cálculo y unidad | Fuente original |
| --- | --- | --- | --- |
| **KPI-01. Crecimiento mensual de ingresos** | Cristopher Quiros | (Ingresos del mes actual − ingresos del mes anterior) ÷ ingresos del mes anterior × 100. **%** | FactSales, DimTime |
| **KPI-02. Ingreso promedio por cliente comprador** | Cristopher Quiros | Ingresos del mes ÷ clientes compradores distintos del mismo mes. **Unidades monetarias por cliente** | FactSales, DimCustomer |
| **KPI-03. Clientes compradores activos por mes** | Jeremy Rodriguez | Clientes distintos con al menos una compra registrada durante el mes. **Número de clientes** | FactSales, DimCustomer, DimTime |
| **KPI-04. Tasa de retención mensual de clientes** | Jeremy Rodriguez | Clientes que compraron en el mes anterior y en el actual ÷ clientes compradores del mes anterior × 100. **%** | FactSales, DimCustomer, DimTime |
| **KPI-05. Crecimiento mensual de unidades vendidas** | Brian Rodriguez | (Unidades vendidas del mes actual − unidades vendidas del mes anterior) ÷ unidades vendidas del mes anterior × 100. **%** | FactSales, DimTime |
| **KPI-06. Concentración de ingresos por género musical** | Brian Rodriguez | Ingresos del género con mayores ingresos del mes ÷ ingresos totales del mes × 100. **%** | FactSales, DimTrack, DimTime |
| **KPI-07. Cantidad de países con ventas mensuales** | Miguel Cruz | Países distintos asociados a clientes que compraron durante el mes. **Número de países** | FactSales, DimCustomer, DimTime |
| **KPI-08. Concentración de ingresos en los cinco artistas principales** | Miguel Cruz | Suma de ingresos de los cinco artistas con mayores ingresos del mes ÷ ingresos totales del mes × 100. **%** | FactSales, DimTrack, DimTime |

Para calcular los KPI-01 a KPI-07 con `data_process.csv`, las columnas candidatas son `FechaFactura` para el mes, `ImporteLinea` para ingresos, `IdCliente` para compradores, `Cantidad` para unidades, `IdGenero` para género y `PaisCliente` para cobertura geográfica. La calidad de estos campos se revisará en el EDA. El KPI-08 requiere enriquecer el CSV con una relación verificada entre `IdCancion` y artista a partir del catálogo de Chinook.

## Pregunta desarrollada y reparto actual

La Fase I desarrolla la propuesta del **KPI-04 de retención**. Al cierre de un mes, ¿qué clientes que compraron ese mes volverán a comprar el siguiente? Cada ejemplo representa un cliente comprador y un mes de corte. `RecompraMesSiguiente` vale 1 si compra durante el mes calendario siguiente y 0 si ese mes es observable y no compra. El equipo debe ratificar esta pregunta antes del entrenamiento.

| Integrante | Trabajo del Proyecto III |
| --- | --- |
| Brian | Fase I. Pregunta de negocio, EDA, construcción de la tabla cliente-mes y diccionario de variables. |
| Jeremy | Fase II. Partición temporal, preprocesamiento y ajuste de regresión logística y árbol de decisión. |
| Miguel | Fase III. Comparación sobre prueba independiente, análisis de errores e importancia de variables. |
| Cristopher | Fase IV. Interpretación de negocio, tres recomendaciones, diapositivas y ensayo. |

Brian y Miguel intercambiaron sus fases el 23 de noviembre de 2026. Jeremy y Miguel intercambiaron las fases II y III el 24 de noviembre de 2026. La tabla anterior de KPIs conserva los responsables del Proyecto II.

## Ejecutar la Fase I

1. Abrir [notebooks/proyecto_3.ipynb](notebooks/proyecto_3.ipynb) en Jupyter o Colab con Python 3 y las bibliotecas pandas, NumPy, Matplotlib 3.10 o posterior y scikit-learn 1.4 o posterior. La ejecución local se comprobó con Matplotlib 3.11.2.
2. Conservar el CSV en `data/data_process.csv`. En Colab, crear la carpeta `data` en el directorio de trabajo y subir allí el CSV. Si se descarga el repositorio completo, ejecutar desde su raíz o desde `notebooks/`.
3. Revisar la celda de configuración. `ULTIMO_MES_RESULTADO_COMPLETO` vale `2013-12`. Se adopta el historial cerrado de la práctica tras conciliar las 2.240 líneas y los importes de las 412 facturas con las exportaciones originales del Lab 4. Diciembre tiene siete facturas por 38,62 UM, coincidentes con el Data Warehouse del Proyecto II.
4. Ejecutar todas las celdas en orden. El notebook comprueba claves, importes, etiquetas y que los predictores se puedan reconstruir usando solo ventas conocidas al cierre. Exporta las tablas y las gráficas del EDA.

### Preparar Python en cada computadora

GitHub comparte el código, los datos y las salidas guardadas del notebook. Las bibliotecas se instalan en el entorno de Python de cada computadora. Una persona que ya tenga las dependencias disponibles puede seleccionar ese entorno y ejecutar el notebook.

En VS Code o Antigravity:

1. Instalar o habilitar las extensiones **Python** y **Jupyter** si el editor las solicita al abrir el notebook.
2. Pulsar **Select Kernel**, elegir **Python Environments** y seleccionar el Python que se utilizará para el proyecto.
3. Si aparece una solicitud para instalar **ipykernel**, aceptar la instalación y esperar a que termine. Este paquete permite ejecutar Python como kernel del notebook.
4. Si falta alguna biblioteca, agregar una celda de código de preparación y ejecutar:

   ```python
   %pip install pandas numpy "matplotlib>=3.10" "scikit-learn>=1.4,<2"
   ```

   `%pip` instala en el entorno del kernel seleccionado. pandas, NumPy y Matplotlib se usan en el EDA. scikit-learn se utiliza en los pipelines, los modelos y las métricas de validación de la Fase II.

5. Cuando termine la instalación, pulsar **Restart**, confirmar si se solicita y después **Run All**.

La celda de instalación sirve para preparar el entorno cuando faltan paquetes. Las instrucciones para preparar cada equipo están en este README y el código del análisis comienza con la carga del CSV.

### Ejecutar las celdas en orden

Al abrir una sesión nueva, usar **Run All** para cargar el CSV, construir las tablas y generar las gráficas en ese orden. Cada celda utiliza variables creadas por las anteriores. Las tablas y figuras visibles al abrir el archivo son salidas guardadas de una ejecución previa. El kernel recupera las variables al volver a ejecutar el código.

| Aviso o error | Qué hacer |
| --- | --- |
| `Select Kernel` pide extensiones | Instalar o habilitar Python y Jupyter. Luego seleccionar un entorno de Python. |
| Se solicita `ipykernel` | Instalarlo en el Python seleccionado y esperar a que el kernel esté disponible. |
| `ModuleNotFoundError: No module named 'matplotlib'` | Ejecutar la celda de instalación anterior, reiniciar el kernel y usar **Run All**. |
| `NameError: name 'resumen_mensual' is not defined` | Ejecutar **Run All** desde el principio para crear las variables antes de dibujar las gráficas. |

En **Google Colab**, abrir el notebook, colocar el CSV en `data/data_process.csv` y ejecutar todas las celdas desde el principio. Si falta una biblioteca, la misma instrucción `%pip` permite instalarla en la sesión de Colab. La preparación de Colab corresponde a su entorno remoto y cada computadora local utiliza su propio entorno.

### Resultados de la Fase I

Se generan **405 filas y 13 columnas**, con 40 recompras. Hay 325 casos anteriores a 2013 y 80 casos de 2013. La tabla está disponible en [resultados/tablas/cliente_mes.csv](resultados/tablas/cliente_mes.csv), junto con el [diccionario](resultados/tablas/diccionario_cliente_mes.csv). Las seis variables numéricas propuestas son recencia, facturas, gasto, diversidad de géneros, antigüedad observada y días de cobertura. El país es la variable categórica. El notebook documenta sus ventanas temporales y la variable de auditoría `Unidades90d`.

El CSV del workshop conserva sus bytes originales. Las exportaciones derivadas se guardan en `resultados/`. El último mes de corte es noviembre de 2013 y su resultado se observa en diciembre de 2013. Los compradores de diciembre requerirían observar enero de 2014 para construir otra cohorte supervisada. La tabla derivada incluye las etiquetas de 2013 para la evaluación final, que Jeremy y Miguel deben reservar al definir el protocolo de prueba.

Se ejecutaron las **13 celdas de código de la Fase I**, incluidas las gráficas, y se revisaron visualmente las cuatro figuras. Las salidas están guardadas dentro del notebook. Las imágenes exportadas son [compras mensuales](resultados/figuras/eda_compras_mensuales.png), [retención mensual](resultados/figuras/eda_retencion_mensual.png), [atípicos](resultados/figuras/eda_atipicos_cliente_mes.png) y [correlaciones](resultados/figuras/eda_correlaciones_cliente_mes.png). El notebook incluye las conclusiones del EDA y el ejemplo rastreable que Brian puede explicar en la defensa. Jeremy completó la partición, el preprocesamiento y el entrenamiento de la Fase II; Miguel continúa con la evaluación y Cristopher con las recomendaciones y la presentación.


## Fase II de Jeremy: preparación y entrenamiento

Jeremy realiza la segunda parte que antes estaba asignada a Miguel. La Fase III
queda a cargo de Miguel. Los responsables de los KPIs del Proyecto II conservan
su asignación original.

1. Preparar el kernel con las instrucciones anteriores y abrir
   `notebooks/proyecto_3.ipynb`.
2. Usar **Restart → Run All**. La Fase I reconstruye la tabla cliente-mes y sus
   cuatro figuras; después se ejecutan las celdas de la Fase II. La conexión a
   PostgreSQL y los archivos de los otros proyectos no se necesitan: la entrada
   es `data/data_process.csv` de este repositorio.
3. Verificar la salida **Desarrollo: 325 casos; 33 recompras** y **Prueba
   reservada: 80 casos**. Desarrollo tiene resultados de 2009–2012. Cada modelo
   se valida con años posteriores a su entrenamiento: 2010, 2011 y 2012.
4. Revisar las tablas de configuración elegida y las dos figuras nuevas. Se
   prueban ocho configuraciones de logística y doce del árbol, con nueve
   umbrales prefijados. El criterio es F1 positivo conjunto de validación. En
   2012 ROC/AUC queda vacía porque no hubo positivos; sus falsas alarmas se
   conservan en el análisis.
5. Al terminar aparecen `modelos_ajustados`, `umbrales_modelos`, `X_prueba` y
   `y_prueba`. Miguel continuará desde esos objetos en la misma sesión para su
   Fase III. En otra sesión debe ejecutar el notebook desde el principio. Los
   modelos se reconstruyen en memoria; no se descargan archivos de modelos.

La preparación se aprende dentro de cada bloque mediante pipelines. País se
codifica sin imponer orden y admite categorías nuevas; las numéricas se imputan
si aparece un faltante y se estandarizan para logística. El árbol utiliza su
escala original. Se conserva el orden cronológico ante el desbalance y se
comparan pesos de clase calculados exclusivamente con entrenamiento.

Se fijaron logística con `C=1`, sin pesos, y umbral `0.1`; árbol con profundidad
máxima `2`, mínimo `10` casos por hoja, sin pesos, y umbral `0.5`. En validación
conjunta sus F1 son aproximadamente `0.3048` y `0.5484`, respectivamente. Son
resultados usados para ajustar; la comparación final y la elección del ganador
corresponden a Miguel sobre los casos reservados de 2013.

### Archivos generados por la Fase II

| Archivo en `resultados/` | Qué contiene |
| --- | --- |
| `tablas/fase2_protocolo.json` | Semilla, fechas, variables, versiones, rejillas, criterio, parámetros y umbrales fijados. |
| `tablas/fase2_particion_cliente_mes.csv` | Clave cliente-mes y asignación de desarrollo/prueba; no incluye etiquetas de prueba. |
| `tablas/fase2_bloques_temporales.csv` | Tamaños y clases de entrenamiento y validación por año. |
| `tablas/fase2_busqueda_validacion.csv` | Los 180 pares de configuración y umbral comparados. |
| `tablas/fase2_configuraciones_elegidas.csv` | Una configuración seleccionada por algoritmo. |
| `tablas/fase2_resumen_validacion.csv` | Resultados de validación de ambos modelos y la referencia mayoritaria. |
| `tablas/fase2_validacion_anual.csv` | Desglose anual, incluidos conteos de errores y AUC no definida en 2012. |
| `tablas/fase2_predicciones_validacion.csv` | Predicciones fuera de entrenamiento rastreables por cliente y mes. |
| `figuras/fase2_particion_temporal.png` | Separación cronológica de los bloques. |
| `figuras/fase2_ajuste_umbrales.png` | Relación entre umbral y F1 de validación para cada configuración elegida. |

La ejecución se verificó con Python 3.13.17, pandas 3.1.1, NumPy 2.5.5,
Matplotlib 3.11.2 y scikit-learn 1.9.1. La Fase II deja reservadas las
predicciones y métricas de prueba de 2013, las importancias y las decisiones de
negocio para las fases siguientes.
