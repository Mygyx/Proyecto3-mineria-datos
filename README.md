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
- `notebooks/` reúne los notebooks de trabajo y será la ubicación de `proyecto_3.ipynb`, que integrará el EDA y preprocesamiento, el modelado, la evaluación y las conclusiones. Antes de entregar, ese notebook debe poder ejecutarse de principio a fin usando el CSV de entrada.
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

Los indicadores sirven para describir el desempeño histórico y formular preguntas de negocio. El equipo aún debe escoger el KPI prioritario y definir qué variable se intentará predecir en el [notebook del proyecto](notebooks/proyecto_3.ipynb).
