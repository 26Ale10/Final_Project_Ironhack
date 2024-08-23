# Modelo de Machine Learnig para medir calidad del agua.

## Tabla de contenidos

- [Introducción](#introducción)
- [Definición del Problema](#Definición-del-problema)
- [Recolección de Datos](#recolección-de-datos)
- [Librerías](#librerías)
- [Algoritmos](#algoritmos)
- [Limpieza y Preparación de Datos](#impieza-y-Preparación-de-Datos)
- [Análisis Exploratorio de Datos](#Análisis-Exploratorio-de-Datos)
- [Construcción y Evaluación de Modelos](#Construcción-y-Evaluación-de-Modelos)
- [Resultados y Discusión](#resultados-y-discusión)
- [Conclusión](#Conclusión)
- [Aprendizajes clave y desafíos](#aprendizajes-clave-y-desafíos)
- [Uso](#Uso)

## Introducción

El agua es esencial para la vida en la Tierra. Representa un componente fundamental de todos los seres vivos y desempeña un papel crucial en numerosos procesos naturales. Desde regular la temperatura del planeta hasta ser el medio donde se desarrollan innumerables formas de vida, el agua es un recurso indispensable. Además, el acceso a agua potable segura es un derecho humano básico y está directamente relacionado con la salud pública, la seguridad alimentaria y el desarrollo socioeconómico.

## Definición del Problema

Se cuenta con un conjunto de datos que describe diversas características del agua, como el pH, la dureza, la presencia de contaminantes, etc. El código se centra en el proceso de análisis y modelado de datos relacionados con la calidad del agua. El objetivo principal es determinar el mejor modelo y parametros que nos permita predecir si un cuerpo de agua es potable o no.

## Recolección de Datos

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

## Construcción y Evaluación de Modelos

El código que se diseño define una serie de pipelines para diferentes modelos de clasificación, junto con una grilla de parámetros para realizar una búsqueda exhaustiva de los mejores hiperparámetros.

### Pipelines:

- **¿Qué es un pipeline?** Un pipeline en scikit-learn es una secuencia de transformaciones y un estimador final. Esto permite encadenar múltiples pasos de preprocesamiento y entrenamiento en un solo objeto.
- **¿Por qué usar pipelines?** Facilitan la gestión de flujos de trabajo de machine learning, desde la preparación de los datos hasta la obtención de predicciones.

### Pipelines definidos:

- `svc_pipeline`, `knn_pipeline`, `tree_pipeline`, `random_forest`, `Logistic_regression`: Cada uno de estos pipelines representa un modelo de clasificación específico (SVC, KNN, árbol de decisión, bosque aleatorio y regresión logística, respectivamente).
- `preprocess`: Este es un transformador (probablemente definido en otra parte del código) que se aplica a los datos antes de entrenar el modelo. Podría incluir tareas como escalamiento, codificación de variables categóricas, selección de características, etc.

### Grilla de parámetros:

- `param_grid`: Esta lista de diccionarios define los diferentes valores que se probarán para cada hiperparámetro de los modelos. Por ejemplo, `'svc__C': [0.1, 1, 10]` significa que se probarán tres valores diferentes para el parámetro de regularización C del modelo SVC.
- Los nombres como `'svc__C'` indican que se está especificando un parámetro del estimador `svc` dentro del pipeline.

### Resumen de lo que hace el código

- **Define múltiples modelos de clasificación:** Se crean pipelines para cada modelo, encapsulando el preprocesamiento y el modelo en sí.
- **Especifica una grilla de parámetros:** Se define una grilla de parámetros para explorar diferentes combinaciones de hiperparámetros para cada modelo.
- **Preparación para la búsqueda de hiperparámetros:** Con esta configuración, estarías listo para utilizar GridSearchCV para encontrar los mejores hiperparámetros para cada modelo, evaluando su rendimiento en un conjunto de validación cruzada.

## Resultados y Discusión

![alt text](<Calidad del Agua/Imagenes/gradicando-modelos2.png>)

_No hubo mucha variación en las capacidades predictivas. SVC fue ligeramente mejor que los otros modelos. Sin embargo, creo que el conjunto de datos es demasiado pequeño para hacer predicciones más precisas._

- **Matrices de confusión del SVC**

![alt text](<Calidad del Agua/Imagenes/conf_SVC_train.png>)

![alt text](<Calidad del Agua/Imagenes/conf_SVC_test.png>)

### Ejes:

- **Eje Y (Clase Real):** Representa la clase real o verdadera de las observaciones.
- **Eje X (Clase Predicha):** Representa la clase que el modelo predijo para cada observación.

### Valores de las celdas:

- **1689:** El modelo clasificó correctamente 1689 observaciones como pertenecientes a la clase 0.
- **99:** El modelo clasificó erróneamente 99 observaciones que en realidad pertenecían a la clase 0, pero las asignó a la clase 1.
- **694:** El modelo clasificó erróneamente 694 observaciones que en realidad pertenecían a la clase 1, pero las asignó a la clase 0.
- **461:** El modelo clasificó correctamente 461 observaciones como pertenecientes a la clase 1.

_Se realizó una prueba eliminando la caracteristicas que presentaba originalmente un 33% de valores nulos pensando que esto podría beneficiar al modelo y mejorar las predicciones, pero, la eliminación de esta caracteristica resto precisión a los modelos._

## Conclusión

La matriz de confusión revela los siguientes puntos clave:

- **Desempeño en la clase 0:** El modelo muestra un desempeño superior en la clasificación de la clase 0.
- **Desequilibrio en la clase 1:** Hay un número considerable de falsos negativos (observaciones de la clase 1 clasificadas como 0).

Si continuara con este conjunto de datos en particular, probaría el pipeline en un conjunto más grande de caracteristicas o algunas caracteristicas nuevas que permitan que el porcentaje de acierto aumente. Aunque teniendo en cuenta el resultado de todos los modelos tambien se podria concluir que los datos no son reales. Esta idea se podria comprobar con un EDA aún mas profundo del realizado o entendiendo mejor el campo profesional.

## Aprendizajes clave y desafíos

Al realizar este proyecto, he podido experimentear cada modelo, especialmente en lo que respecta a sus parámetros y cómo acceder a ellos(aunque esto se me sigue haciendo cuesta arriba).

Si bien el curso proporcionó una base sólida, la verdadera comprensión de todo estos conceptos se logra a través de la aplicación práctica en múltiples proyectos reales.

**Construyendo pipelines:**

La creación de modelos individuales resultó ser más sencilla que la construcción de pipelines. La principal dificultad radica en **extraer los parámetros** de cada modelo dentro del pipeline.

## Uso
