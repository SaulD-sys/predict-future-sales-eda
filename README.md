# Predict Future Sales: Análisis Exploratorio de Datos (EDA)

<a target="_blank" href="https://cookiecutter-data-science.drivendata.org/">
    <img src="https://img.shields.io/badge/CCDS-Project%20template-328F97?logo=cookiecutter" />
</a>

Proyecto #1 del curso **Product Development** (Maestría). Es un análisis exploratorio del dataset
[Predict Future Sales](https://www.kaggle.com/competitions/competitive-data-science-predict-future-sales/data)
de Kaggle, que prepara el terreno para una futura etapa de *forecasting* de ventas mensuales por tienda y producto.

> Este repositorio contiene **solo el EDA**. No incluye ningún modelo predictivo.

## Dataset

Ventas diarias de la cadena rusa de tiendas 1C Company, de enero de 2013 a octubre de 2015:

| Archivo | Contenido |
|---|---|
| `sales_train.csv` | Ventas diarias históricas (una fila por producto, tienda y día) |
| `items.csv` | Catálogo de productos |
| `item_categories.csv` | Catálogo de categorías |
| `shops.csv` | Catálogo de tiendas |
| `test.csv` | Pares tienda-producto a predecir (noviembre 2015) |

Los datos (unos 100 MB) **no se versionan**: `.gitignore` excluye los CSV, el ZIP y el contenido de `data/raw/`.

## Estructura del repositorio

Estructura generada con la plantilla oficial **Cookiecutter Data Science** (v2.3.0):

```
├── data
│   ├── external        <- Datos de terceros (no usado)
│   ├── interim         <- Datos intermedios (no usado; el EDA trabaja en memoria)
│   ├── processed       <- Datos finales para modelado (no usado)
│   └── raw             <- Archivos originales de Kaggle (no versionados)
├── docs                <- Documentación
├── models              <- Modelos entrenados (vacío: este proyecto no entrena modelos)
├── notebooks
│   └── 01_exploratory_data_analysis.ipynb   <- Notebook del EDA, ejecutado
├── references          <- Material de referencia
├── reports
│   └── figures         <- Figuras para reportes
├── src                 <- Paquete de código del proyecto
├── Makefile            <- Comandos de conveniencia de la plantilla
├── pyproject.toml      <- Metadatos y dependencias del proyecto
└── README.md
```

## Requisitos

- **Python 3.12** (el análisis se ejecutó con Python 3.12.13).
- Librerías: `pandas`, `numpy`, `matplotlib`, `seaborn`, `statsmodels`, `scipy`, `jupyter` e `ipykernel`. Están declaradas en `pyproject.toml`.
- Se recomienda [uv](https://docs.astral.sh/uv/) para crear el entorno.

## Cómo reproducir el análisis

1. **Clonar el repositorio**

   ```bash
   git clone https://github.com/SaulD-sys/predict-future-sales-eda.git
   cd predict-future-sales-eda
   ```

2. **Crear el entorno virtual e instalar las dependencias**

   ```bash
   uv venv .venv --python 3.12
   uv pip install --python .venv pandas numpy matplotlib seaborn statsmodels scipy jupyter ipykernel
   ```

3. **Descargar los datos de Kaggle.** Hace falta una cuenta gratuita y aceptar las reglas de la competencia.
   - Descarga `competitive-data-science-predict-future-sales.zip` desde la
     [página de datos de la competencia](https://www.kaggle.com/competitions/competitive-data-science-predict-future-sales/data).
   - Extrae su contenido **directamente** en `data/raw/`, de forma que queden
     `data/raw/sales_train.csv`, `data/raw/items.csv`, `data/raw/item_categories.csv`,
     `data/raw/shops.csv` y `data/raw/test.csv`.
   - No subas estos archivos al repositorio. `.gitignore` ya los excluye.

4. **Ejecutar el notebook**
   - **VS Code:** abre `notebooks/01_exploratory_data_analysis.ipynb`, selecciona el kernel de `.venv` (Python 3.12) y ejecuta *Run All*.
   - **Línea de comandos:**

     ```bash
     .venv/Scripts/jupyter nbconvert --to notebook --execute --inplace notebooks/01_exploratory_data_analysis.ipynb
     ```

     En macOS o Linux, usa `.venv/bin/jupyter`.

   El notebook lee los CSV en modo de solo lectura y aplica todas las transformaciones en memoria. Los archivos originales no se modifican.

## Contenido del EDA

El notebook sigue la numeración de las instrucciones del proyecto:

| Sección | Contenido |
|---|---|
| 1 | Estructura del proyecto y repositorio |
| 2 | Comprensión inicial: carga, dimensiones, diccionario de datos, variable objetivo y rango temporal |
| 3 | Validación de estructura: tipos, conversión de fechas, frecuencia temporal y `date_block_num` |
| 4 | Faltantes, valores inválidos y duplicados. Decisiones de limpieza, todas trazables y conciliadas (exclusión de 6 duplicados exactos, imputación de 1 precio negativo, unificación de 3 pares de tiendas duplicadas; se conservan las devoluciones) |
| 5 | Análisis descriptivo: estadísticos y distribución por producto, categoría, tienda y periodo |
| 6 | Exploración temporal: tendencia, estacionalidad, picos y caídas, ciclos semanales y anuales |
| 7 | Comparativo de productos y tiendas, y detección de *outliers* con criterios explícitos |
| 8 | Visualizaciones obligatorias: serie de tiempo, barras por tienda, producto y categoría, y *heatmaps* |
| 9 | ACF y PACF de la serie total (mensual y diaria) y de tiendas, productos y pares tienda-producto seleccionados |
| 10 | Insights: variables relevantes, patrones para el *forecasting* (incluido el % de pares de `test` con historial) y calidad del dataset |

## Uso de inteligencia artificial

De acuerdo con las instrucciones del proyecto, en su desarrollo se utilizó **Claude Code** dentro de VS Code.
