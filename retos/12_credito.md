# Reto concesión de crédito

Vamos a crear una serie de modelos de predicción sobre un dataset de impagos publicado hace años en Kaggle.

En este repositorio, tienes disponible:

* Los datos en `dat/credit.csv`
* Una breve explicación de qué es cada columna en `dat/credit-data-dictionary.xls`

Antes de ponerte a modelizar, dedica un rato a explorar los datos, cómo se distribuyen sus columnas, donde hay nulos, ...

## Contexto

Utilizaremos modelos basados en árboles, especialmente los random forest. Es muy recomendable que leas [este artículo](https://www.analyticsvidhya.com/blog/2016/04/complete-tutorial-tree-based-modeling-scratch-in-python/#nine). No tiene desperdicio, pero si no puedes leerlo completo, ve directo al punto 9 - ¿qué son los random forest?.

## Los modelos

El objetivo es ir creando varios modelos e intentar mejorar la precisión de la predicción. Acabaremos teniendo varios ficheros que nombraremos consecutivamente: `01.[R/py]`, `02.[R/py]`, etc.

Es recomendable evitar que el efecto aleatorio de operaciones que hacemos en los modelos varíe la precisión de una vez a otra. Por eso, te recomiendo que fijes la semilla al principio del script. De esta forma, si ejecutas todo el script, los resultados serán los mismos (es decir, será reproducible). Lo puedes hacer en R con `set.seed(1234)` o Python con `random.seed(1234)`.

La medida de evaluación que utilizaremos es el AUC o área bajo la curva. Hay varios paquetes que te permiten calcularla, investiga y elige la forma que más te guste.

Además, especialmente cuando creemos nuevas columnas que entran al entrenamiento, es interesante mirar la importancia de variables. Si nuestras nuevas columnas cobran importancia, significa que tiene poder predictivo y lo más probable es que estemos mejorando el modelo. Lo podemos hacer con `varImpPlot` en R o `feature_importances_` en Python. Para Python, hay un ejemplo completo [aquí](http://scikit-learn.org/stable/auto_examples/ensemble/plot_forest_importances.html) sobre cómo pintar el gráfico.

## Estructura general

Todos los modelos deberán hacer lo siguiente. Es recomendable que saques el código común a funciones que importes.

1. Fija la semilla
2. Lee los datos del CSV
3. Elimina las variables innecesarias (X)
4. Preprocesa los datos y separa en entrenamiento (70%) y validación (30%): variable en cada modelo, ya que vamos a probar diferentes ideas
5. Entrena el modelo con el conjunto de entrenamiento
6. Pinta la importancia de variables.
7. Mide el AUC en el conjunto de validación. Déjalo apuntado con un comentario al final del script y comenta brevemente si ves mejora o no en el resultado y por qué crees que pasa.

### Modelo 01

* Preproceso: imputa los nulos de `NumberOfDependents` con la moda de su columna y `MonthlyIncome` con un cero.
* Modelo: entrena un random forest de 100 árboles

### Modelo 02

* Preproceso: lo mismo que en el modelo anterior pero, además, balancea las clases del conjunto de entrenamiento. Es decir, debe haber las mismas observaciones de impago que de pago correcto. Esto nos puede servir para que el algoritmo tenga sesgo hacia la clase predominante (pago correcto)
* Modelo: entrena un random forest de 100 árboles

¿Se observa una mejora?

### Modelo 03

* Preproceso: lo mismo que en el modelo anterior
* Modelo: entrena un random forest de 500 árboles

¿Se observa una mejora?

### Modelo 04

* Preproceso: lo mismo que en el modelo anterior pero, además, crea dos nuevas columnas con valor true/false indicando si esa fila tiene `NumberOfDependents` y `MonthlyIncome` nulos respectivamente (llámalas `UnknownNumberOfDependents` y `UnknownMonthlyIncome`). Si estas nuevas columnas cobran importancia en el modelo, querrá decir que probablemente sea un indicativo de impago (p.e. en caso de que la gente elija dar o no el dato y, si tienen premeditación en no pagar, prefieran omitirlo)
* Modelo: entrena un random forest de 500 árboles

¿Tienen importancia las nuevas variables que hemos introducido? ¿Se observa una mejora?

### Modelo 05

* Preproceso: lo mismo que en el modelo anterior pero, además, vamos a arreglar la columna `DebtRatio` y crear columnas relacionadas. Fíjate que, aunque debería tener un valor entre 0 y 1, a veces tiene valores muy altos. Haz lo siguiente:

    * Crea la columna `ZeroDebtRatio` que tenga valor true si DebtRatio es igual a 0, false si no. De esta manera, nos guardamos si el valor original era cero antes de corregirlo, y no perdemos la importancia que pudiera tener.
    * Pon el valor de `DebtRatio` a cero si `UnknownMonthlyIncome` es true, para corregir los valores altos al desconocer los ingresos.
    * Vamos a probar otra idea relacionada, que es calcular la deuda que tiene la persona, con una ligera variación. Cuando los valores pueden estar en escalas diferentes, y solo nos importan las diferencias grandes (si tienen más o menos ceros, por así decirlo), podemos usar el logaritmo del valor. Crea una variable `LogDebt` que sea el logaritmo de la deuda (`log(MonthlyIncome * DebtRatio)`). Cuidado con los infinitos al usarlo los logaritmos: sustituye los que te hayan salido por 0.

* Modelo: entrena un random forest de 500 árboles

¿Tienen importancia las nuevas variables que hemos introducido? ¿Se observa una mejora?

### Modelo 06 y siguientes

Crea unos cuantos modelos nuevos con pruebas que se te ocurran. P.e.: usar modelos más simples como los árboles de decisión o más complejos como los Gradient Boost Machine. O crear nuevas columnas que pienses que pueden resultar de interés, y razona la evolución de los resultados. ¿Tu modelo mejora o empeora? ¿Por qué crees que puede ser?
