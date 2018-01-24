# Reto datos de tiroteos masivos en EEUU

Casi todos los conjuntos de datos con los que nos encontramos, traen problemas de limpieza a solucionar:

* Conversión de tipos: normalmente, de string a lo que el valor represente: números con o sin decimal, fechas u otros
* Eliminación de duplicados
* Tratamiento de valores nulos: mediante eliminación de la fila o imputando algún valor
* Estandarización de valores. P.e. en una misma columna que representa el sexo, podemos encontrarnos con valores que representan lo mismo pero están introducidos de forma diferente. Estas diferencias pueden estar causadas por mayúsculas / minúsculas, uso de abreviaturas, diferentes idiomas, ... P.e. para expresar la situación soltero en el estado civil, podemos encontrar: soltero, Soltero, single, ...
* Eliminación de valores imposibles. P.e. si nos encontramos entre los datos una persona de 2 años de edad con altura 1.80 metros.

Vamos a limpiar un dataset que tiene varios de estos problemas.

La carpeta con la solución a este reto debería ser: `07_tiroteos_eeuu`.

He dejado los datos en este mismo repositorio, en `retos/dat/us_mass_shootings.csv`. Cópialo a una carpeta `dat/` dentro de `07_tiroteos_eeuu`.

## Limpieza

Lee el CSV y explora los datos:

* Cómo se distribuyen las columnas numéricas
* Cantidad de nulos
* Valores diferentes de columnas de clases (sexo, raza, ...)

**NOTA**: cuidado con los factors en R. Es más fácil leerlo todo como string y, luego, convertir cosas como el sexo o la raza a factor. Lo comento porque funciones como `read.csv`, por defecto, leen los strings como factors (mira en la ayuda el argumento `stringsAsFactors`)

Una vez hayas hecho tu análisis exploratorio (no es necesario que incluyas el código en el script final), haz un script que haga lo siguiente:

* Lea el CSV
* Convierta correctamente los tipos de datos: las fechas y los números
* Convierta la columna `Mental.Health.Issues` a un valor booleano (en R, logical). Los valores unclear, unknown y otros deben pasarse a NA.
* Estandarice las columnas de clases al mínimo de valores posibles y las convierta a tipo factor (R) o categorical (Python). Estas columnas son:

    * `Race`: los valores que queremos tener son: `white`, `black`, `asian`, `other`. Algunos ejemplos de la transformación:

        * `Black American or African American` debe ser `black`
        * `Some other race`, las mezclas de razas y cosas minoritarias que no aplican en los otros grupos (como `Latino` o `Native American or Alaska Native`) deben ser `other`
        * `Unknown` debe ser NA

    * `Gender`: los valores que queremos tener son: `male`, `female`, `male/female`. Los unknown deben ser NA.

* Separa la columna `Location` en `City` y `State`. Algunos comentarios:

    * Hay una fila que solamente tiene el valor `Washington D.C.` en su columna de localzación. Puedes convertirlo a `Washington, Washington` antes de hacer la separación.
    * Están ambos valores separados por coma. Pero ten cuidado, no es tan simple como coger como `City` lo de la derecha y como `State` lo de la izquierda de la coma. Hay valores que tiene varias comas. Escoge una solución robusta de separación que no rompa los casos especiales. Cuidado con Washington (tanto en ciudad como estado), hay un caso especial que debes estandarizar.

* A veces las columnas de `Fatalities` y `Injured` no suman `Total.victims`. Actualiza esta última para que sea la suma de las otras dos.
* Elimina los duplicados para un mismo estado y fecha.

## Ejercicio opcional

Verás que hay algunas observaciones que tienen un nulo en el estado pero no en latitud y longitud. Utiliza una API de geolocalización inversa para, en base a esos datos, imputar la columna de estado.

Después, estandariza el estado. Tendrás mezcla de abreviaturas y nombres completos (p.e. CA y California). Dependiendo del resultado de la API, es posible que también tengas mezclas de mayúsculas y minúsculas. Para ayudarte a esta tarea, puedes buscar un dataset para convertir de uno a otro, como el disponible [aquí](https://github.com/jasonong/List-of-US-States/blob/master/states.csv). Si decides usarlo, guárdalo también en la carpeta `dat/`

