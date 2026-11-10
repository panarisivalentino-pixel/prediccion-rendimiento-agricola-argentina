# Rendimiento agrícola y zonas agroclimáticas de Argentina (1981–2024)

Proyecto de ciencia de datos que analiza 44 años de estimaciones agrícolas de Argentina para entender **qué determina el rendimiento de los cultivos (kg/ha)**, predecirlo con machine learning y descubrir **zonas agroclimáticas** sin usar datos geográficos.

Trabajo grupal de la **Tecnicatura Universitaria en Ciencia de Datos e Inteligencia Artificial** (Universidad del Gran Rosario).

## Resultados principales

| Métrica | Valor |
|---|---|
| Registros analizados | 111.417 (cultivo × departamento × año) |
| Mejor modelo | LightGBM (6 modelos comparados) |
| Variación del rendimiento explicada (R²) | 94 % |
| Error promedio (MAE) | 500 kg/ha, la mitad que un modelo lineal |
| Pronóstico de años futuros (2016–2024) | R² de 72 % |
| Zonas agroclimáticas encontradas | 5 |

- **La producción está muy concentrada:** soja, maíz y trigo suman el 77 % de las toneladas; Buenos Aires, Córdoba y Santa Fe, el 71 %.
- **El rendimiento creció fuerte en 40 años:** el del maíz casi se duplicó, de 3.311 a 6.561 kg/ha.
- **El cultivo y la tecnología pesan más que el clima:** el tipo de cultivo explica el 58 % de las diferencias de rendimiento y el clima, el 12 % (análisis SHAP).
- **El clima tiene efectos claros:** por encima de 20 °C de media anual el rendimiento cae, y la lluvia óptima está entre 800 y 1.100 mm por año.
- **Los datos reconstruyen el mapa agroclimático del país:** agrupando departamentos solo por su clima aparecen la pampa húmeda, la Mesopotamia, el norte cálido, Cuyo y la Patagonia.

## Datos

- **Estimaciones agrícolas** del Ministerio de Agricultura, Ganadería y Pesca (MAGyP): superficie sembrada y cosechada, producción y rendimiento por cultivo, provincia y departamento.
- **Clima anual por provincia** de [NASA POWER](https://power.larc.nasa.gov/): temperatura, radiación solar, humedad relativa y lluvia.

Las dos fuentes se limpiaron por separado y se unieron por provincia y año.

## Notebooks

| # | Notebook | Contenido |
|---|---|---|
| 01 | [Limpieza agro](notebooks/01_limpieza_agro.ipynb) | Limpieza de las estimaciones agrícolas del MAGyP |
| 02 | [Limpieza clima](notebooks/02_limpieza_clima.ipynb) | Limpieza de los datos climáticos de NASA POWER |
| 03 | [Unión de datasets](notebooks/03_union_datasets.ipynb) | Integración de ambas fuentes en una sola tabla |
| 04 | [Análisis agro](notebooks/04_analisis_agro.ipynb) | Análisis exploratorio de la producción |
| 05 | [Análisis clima](notebooks/05_analisis_clima.ipynb) | Análisis exploratorio del clima |
| 06 | [Dashboard](notebooks/06_dashboard_graficos_agro.ipynb) | Visualizaciones interactivas de la producción agrícola |
| 07 | [Modelado supervisado](notebooks/07_modelado_supervisado.ipynb) | Comparación de modelos, optimización e interpretabilidad (SHAP) |
| 08 | [Red neuronal](notebooks/08_red_neuronal_mlp.ipynb) | Perceptrón multicapa comparado con los modelos de árboles |
| 09 | [No supervisado](notebooks/09_no_supervisado_zonas_agroclimaticas.ipynb) | PCA + clustering para encontrar zonas agroclimáticas |

## Metodología

1. **Limpieza e integración:** se trabajó solo con años con clima medido (1981–2024) y se evitó el doble conteo de cultivos.
2. **Análisis exploratorio** de la producción, el rendimiento y el clima.
3. **Modelado supervisado:** regresión lineal, Ridge, Random Forest, Gradient Boosting, LightGBM y una red neuronal, con optimización de hiperparámetros, validación cruzada y una validación temporal (entrenamiento hasta 2015, prueba 2016–2024).
4. **Interpretabilidad** con SHAP para medir qué variables explican cada predicción.
5. **Aprendizaje no supervisado:** PCA sobre el clima de cada departamento y agrupamiento jerárquico y K-Means (K = 5).

## Herramientas

Python · Pandas · NumPy · Scikit-learn · LightGBM · SHAP · Matplotlib · Seaborn · Plotly · Google Colab

## Equipo

Juan Eduardo Botto · Lucas Cesa · Máximo Linzuain · Valentino Panarisi · Santiago Scozziero

Valentino Panarisi desarrolló el análisis no supervisado de zonas agroclimáticas; el resto del proyecto se realizó en conjunto.
