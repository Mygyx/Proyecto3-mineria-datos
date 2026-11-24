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
- `notebooks/proyecto_3.ipynb` contiene la introducción y la Fase I de Brian, con el EDA y la construcción de la tabla cliente-mes. Las siguientes fases del equipo se incorporarán al mismo notebook. Antes de entregar, debe poder ejecutarse de principio a fin usando el CSV de entrada.
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
| Miguel | Fase II. Partición temporal, preprocesamiento y ajuste de regresión logística y árbol de decisión. |
| Jeremy | Fase III. Comparación sobre prueba independiente, análisis de errores e importancia de variables. |
| Cristopher | Fase IV. Interpretación de negocio, tres recomendaciones, diapositivas y ensayo. |

Brian y Miguel intercambiaron sus fases el 23 de noviembre de 2026. La tabla anterior de KPIs conserva los responsables del Proyecto II.

## Ejecutar la Fase I

1. Abrir [notebooks/proyecto_3.ipynb](notebooks/proyecto_3.ipynb) en Jupyter o Colab con Python 3 y las bibliotecas pandas, NumPy y Matplotlib 3.10 o posterior. La ejecución local se comprobó con Matplotlib 3.11.2.
2. Conservar el CSV en `data/data_process.csv`. En Colab, crear la carpeta `data` en el directorio de trabajo y subir allí el CSV. Si se descarga el repositorio completo, ejecutar desde su raíz o desde `notebooks/`.
3. Revisar la celda de configuración. `ULTIMO_MES_RESULTADO_COMPLETO` vale `2013-12`. Se adopta el historial cerrado de la práctica tras conciliar las 2.240 líneas y los importes de las 412 facturas con las exportaciones originales del Lab 4. Diciembre tiene siete facturas por 38,62 UM, coincidentes con el Data Warehouse del Proyecto II.
4. Ejecutar todas las celdas en orden. El notebook comprueba claves, importes, etiquetas y que los predictores se puedan reconstruir usando solo ventas conocidas al cierre. Exporta las tablas y las gráficas del EDA.

Se generan **405 filas y 13 columnas**, con 40 recompras. Hay 325 casos anteriores a 2013 y 80 casos de 2013. La tabla está disponible en [resultados/tablas/cliente_mes.csv](resultados/tablas/cliente_mes.csv), junto con el [diccionario](resultados/tablas/diccionario_cliente_mes.csv). Las seis variables numéricas propuestas son recencia, facturas, gasto, diversidad de géneros, antigüedad observada y días de cobertura. El país es la variable categórica. El notebook documenta sus ventanas temporales y la variable de auditoría `Unidades90d`.

El CSV del workshop conserva sus bytes originales. Las exportaciones derivadas se guardan en `resultados/`. El último mes de corte es noviembre de 2013 y su resultado se observa en diciembre de 2013. Los compradores de diciembre requerirían observar enero de 2014 para construir otra cohorte supervisada. La tabla derivada incluye las etiquetas de 2013 para la evaluación final, que Miguel y Jeremy deben reservar al definir el protocolo de prueba.

Se ejecutaron las **13 celdas de código de la Fase I**, incluidas las gráficas, y se revisaron visualmente las cuatro figuras. Las salidas están guardadas dentro del notebook. Las imágenes exportadas son [compras mensuales](resultados/figuras/eda_compras_mensuales.png), [retención mensual](resultados/figuras/eda_retencion_mensual.png), [atípicos](resultados/figuras/eda_atipicos_cliente_mes.png) y [correlaciones](resultados/figuras/eda_correlaciones_cliente_mes.png). El notebook incluye las conclusiones del EDA y el ejemplo rastreable que Brian puede explicar en la defensa. Miguel continúa con la partición y el preprocesamiento acordados, Jeremy con la evaluación y Cristopher con las recomendaciones y la presentación.
