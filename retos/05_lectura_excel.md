# Reto lectura automatizada de Excel

Aunque no es el formato ideal, muchas veces nos toca leer de Excel. En R, la mejor alternativa es `readxl` y en Python, el propio `pandas` tiene una función `read_excel` útil para estos casos.

En este reto vamos a leer automáticamente datos de población anual, publicados por el INE. Los datos están disponibles en la siguiente URL: http://www.ine.es/pob_xls/pobmun.zip . El objetivo es, a partir de este archivo comprimido, devolver como formato .csv los datos de todos los años en un único fichero.

Esto tiene una complicación extra, muy común al leer ficheros que se suponen que deberían tener el mismo formato: que no lo tienen. Si te fijas, hay años en que los datos empiezan en la fila 2, otros en la 3, y otros en la 4. También el número de columnas es variable.

## 1. Extracción del año

Crea una función `get_year` que, en base al nombre del fichero Excel que leerás (pobmun96.xlsx, pobmun13.xls, etc) te devuelva el año al que pertenece: 1996, 2013, ...

Para hacerlo, puedes utilizar expresiones regulares. Si nunca has trabajado con ellas, puedes coger posiciones fijas de la cadena de texto, y convertirlo.

Como solo vienen dos cifras para indicar un año de 4, puedes suponer que a las superiores o iguales a 90, hay que sumar 1900, y a las inferiores, hay que sumar 2000.

## 2. Gestión de las diferencias en las filas

En la mayor parte de los ficheros, los datos empiezan en la fila 3 (ignorando filas en blanco y la cabecera), pero hay en algunos ficheros que es en la 2 o en la 4.

Crea dos variables, una `first_row_data_default` con el dato por defecto, que es 3, y otra `first_row_data_exceptions` que sea un vector con nombres (R) o diccionario (Python), cuyo nombre / clave sea el año con la excepción y el valor sea la fila donde empieza (2 o 4). Las excepciones son:

* 1998: 2
* 2009: 2
* 2012: 4
* 2013: 4
* 2014: 4
* 2015: 4

Ahora crea una función `get_first_row` que acepte por parámetro un año y devuelva la fila en la que empiezan los datos (2 o 4 si se encuentra el año en cuestión entre nuestras excepciones, o 3 en caso contrario).

NOTA: en Python sí podemos utilizar claves numéricas en los diccionarios, pero en R, los nombres del vector deben ser cadenas de texto. Si usas R, esto te forzará a convertir el año en cadena de caracteres para acceder al valor que le corresponde. p.e., haciendo `first_row_data_exceptions[as.character(2010)]`

## 3. Lectura del excel

Crea una función `read_population` que acepte por argumentos la ruta del fichero y el año al que corresponde, y devuelva un dataframe como salida. Las 3 columnas a extraer en ese dataframe son: 

* `cod_provincia`: el código numérico de la provincia
* `cod_municipio`: el código numérico del municipio
* `poblacion`: la población global

Dentro de esta función, vas a tener que utilizar la creada en el apartado anterior, para saber en qué fila empezar a leer.

Además, a veces hay diferencias en las columnas. La lógica puede ser:

* Si hay 6 columnas, tengo que leer la primera, segunda y cuarta
* Si no, leo la primera, tercera y quinta

Y también hay que quitar las columnas totales que a veces hay entre medias. Esto se puede hacer eliminando todas aquellas filas que no tengan asignada cualquiera de las 3 filas leídas.

## 4. Lectura del archivo comprimido

Ahora, vamos a automatizar la lectura del archivo comprimido. Crea una función que se llame `read_population` (sin argumentos de entrada), que haga lo siguiente:

* Se descargue el fichero `http://www.ine.es/pob_xls/pobmun.zip`
* Lo descomprima e itere sobre los ficheros contenidos. Para cada uno, hará:

    * Extrae el año del nombre, usando la función que hemos creado `get_year`
    * Lee el contenido del excel, usando `read_population`
    * Añada al dataframe devuelto una columna con el año. Es decir, si acabamos de leer los datos de 2015, al dataframe de 3 columnas le añadimos una más que sea `anno` con valor 2015 para todo ese dataframe

* Una todos los dataframes devueltos en uno
* Escriba en disco el dataframe resultante en formato .csv, que tendrá 4 columnas (código provincia, código municipio, población y año).
* Borre todos los archivos temporales (el zip descargado, su contenido, etc), de forma que el único fichero generado extra al ejecutar la función sea el .csv resultado
