# Modelo de Machine Learnig para medir calidad del agua.

## Tabla de contenidos

- [Introducción](#introducción)
- [Definición del Problema](#Definición-del-problema)
- [Recolección de Datos](#recolección-de-datos)
- [Limpieza y Preparación de Datos](#impieza-y-Preparación-de-Datos)
- [Análisis Exploratorio de Datos](#Análisis-Exploratorio-de-Datos)
- [Ingeniería de Características](#Ingeniería-de-Características)
- [Construcción y Evaluación de Modelos](#Construcción-y-Evaluación-de-Modelos)
- [Visualización de Datos y Dashboards](#isualización-de-Datos-y-Dashboards)
- [Resultados y Discusión](#Resultados-y-Discusión)
- [Conclusión](#Conclusión)
- [Future Work](#Future-Work)
- [Instalación](#Instalación)
- [Uso](#Uso)
- [Contribuyendo](#Contribuyendo)
- [Licencia](#Licencia)

## Introducción

## Definición del Problema

## Recolección de Datos

Explique los conjuntos de datos utilizados, incluidas las fuentes y los métodos de recopilación de datos.

| Feature         | Description                                      | Units         |
| --------------- | ------------------------------------------------ | ------------- |
| pH              | pH of water                                      | dimensionless |
| Hardness        | Capacity of water to precipitate soap            | mg/L          |
| Solids          | Total dissolved solids                           | ppm           |
| Chloramines     | Amount of Chloramines                            | ppm           |
| Sulfate         | Amount of Sulfates dissolved                     | mg/L          |
| Conductivity    | Electrical conductivity of water                 | μS/cm         |
| Organic_carbon  | Amount of organic carbon                         | ppm           |
| Trihalomethanes | Amount of Trihalomethanes                        | μg/L          |
| Turbidity       | Measure of light emitting property of water      | NTU           |
| Potability      | Indicates if water is safe for human consumption | boolean       |

## Librerías

<li>pandas
<li>matplotlib
<li>seaborn
<li>plotly
<li>scikit-learn
<li>xgboost
  
## Algoritmos
<li>Logistic Regression
<li>K Nearest Neighbours
<li>Support Vector Machine
<li>Decision Tree
<li>Random Forest
<li>XGBoost

## Limpieza y Preparación de Datos

![alt text](<Calidad del Agua/Imagenes/Valores-nulos.png>)

- Hay 491 valores nulos en la columna 'ph', lo que significa un 17.63% de los datos
- Hay 781 valores nulos en la columna 'Sulfate', lo que significa un 31.30% de los datos
- Hay 162 valores nulos en la columna 'Trihalomethanes', lo que significa un 5.20% de los datos

![alt text](<Calidad del Agua/Imagenes/Comparacion-de-densidades-de-probabilidad-del-pH.png>)

_El gráfico muestra que rellenar los valores faltantes con la media puede alterar la distribución original de los datos, especialmente en las colas._

![alt text](<Calidad del Agua/Imagenes/relleno-cuadratico.png>)

_La gráfica sugiere que el método de interpolación cuadrática ha sido exitoso en preservar las características principales de la distribución del pH._

## Análisis Exploratorio de Datos

![alt text](<Calidad del Agua/Imagenes/matriz-de-correlacion.png>)

### Análisis de la matriz de correlación

- **Correlaciones débiles:** La mayoría de las variables presentan correlaciones débiles, lo que indica que no existe una relación lineal fuerte entre ellas.
- **Correlaciones moderadas:** Algunas variables, como 'Hardness' y 'Solids', muestran una correlación positiva moderada, sugiriendo una relación directa.
- **Posibles relaciones inversas:** La potabilidad parece estar relacionada negativamente con variables como 'Sulfate_cuadratica' y 'ph_cuadratica'.

## Ingeniería de Características

Describa el proceso de creación de nuevas características y cualquier técnica de selección de características utilizada.

## Construcción y Evaluación de Modelos

Describa los modelos utilizados, los procesos de entrenamiento y prueba y las métricas de evaluación.

## Resultados y Discusión

![alt text](<Calidad del Agua/Imagenes/gradicando-modelos.png>)

_Al final, no hubo mucha variación en las capacidades predictivas. SVC fue ligeramente mejor que los otros modelos. Sin embargo, creo que el conjunto de datos es demasiado pequeño para hacer predicciones más precisas._

_Se realizó una prueba eliminando la caracteristicas que presentaba originalmente un 33% de valores nulos pensando que esto podría beneficiar al modelo y mejorar las predicciones, pero, la eliminación de esta caracteristica resto precisión a los modelos._

## Conclusión

Aprendí mucho más sobre cada modelo mientras realizaba este proyecto. En particular, sobre sus parámetros y cómo acceder a ellos.

El curso proporcionó una base sólida, pero nunca se pueden entender completamente los conceptos hasta que se aplican en muchos proyectos reales.

Realizar cada modelo individualmente fue mucho más fácil que ponerlos todos en un pipeline. Al construir el pipeline, la parte más difícil es extraer los parámetros para cada modelo. Hay tanta abstracción involucrada en el pipeline que hace que sea muy difícil entender cómo acceder a los resultados.

## Trabajo Futuro

Si continuara con este conjunto de datos en particular, probaría el pipeline en un conjunto más grande de caracteristicas o algunas caracteristicas nuevas que permitan que el porcentaje de acierto aumente.

## Licencia
