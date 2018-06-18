# Reto predicción de lluvia

Vamos a crear una serie de modelos sobre un problema de regresión: predecir la cantidad de lluvia según otros factores metereológicos.

En este repositorio, tienes disponibles los datos en `dat/weather.csv`. Nuestra variable objetivo es `rain`.

El resultado a este ejercicio deberá entregarse en un `Rmd` o notebook de python.

## Semilla

Es recomendable evitar que el efecto aleatorio de operaciones que hacemos en los modelos varíe la precisión de una vez a otra. Por eso, te recomiendo que fijes la semilla al principio del script. De esta forma, si ejecutas todo el script, los resultados serán los mismos (es decir, será reproducible). Lo puedes hacer en R con `set.seed(1234)` o Python con `random.seed(1234)`.

## Exploración y limpieza

Primero, haz la limpieza de datos que creas conveniente. Luego, explora los datos con el objetivo de comprender bien el dataset, observar posibles outliers y afinar la limpieza.

## Entrenamiento y validación

Antes de empezar a modelar y comparar resultados, separa tu dataset en dos: entrenamiento (70%) y validación (30%).

## Los modelos

Vamos a hacer una serie de modelos de regresión y a compararlos. Utilizaremos las siguientes dos métricas:

* MAE o Mean Absolute Error
* RMSE o Root Mean Square Error

Recuerda que siempre entra al algoritmo el dataset de entrenamiento, y estas métricas se miden únicamente con el de validación.

### Modelo 01: línea base

Habitualmente se utiliza como línea base de comparación un modelo que tenga sentido pero muy simple. En este caso, este modelo puede ser el valor medio de `rain` en el dataset de entrenamiento.

Calcula las dos métricas (MAE, RMSE) que da usar este valor en el conjunto de validación. El objetivo en los siguientes modelos será bajar de estos valores de error.

### Modelo 02: regresión lineal

Crea un modelo de regresión lineal y calcula el rendimiento (MAE, RMSE).

_Opcional_: prueba variantes del modelo, como diferentes estrategias de normalización.

### Modelo 03: árboles de decisión de regresión

Crea un modelo con árboles de decisión y calcula el rendimiento.

_Opcional_: prueba variantes del modelo, como podar el árbol.

### Modelo 04: random forests de regresión

Crea un modelo con random forests y calcula el rendimiento.

### Conclusiones

Explica brevemente los resultados observados.
