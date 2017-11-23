# Reto web scraping

En datacamp vamos a aprender cómo leer datos de fuentes estructuradas:

* Ficheros de texto estructurados (CSV y similar)
* Excel
* Bases de datos

Y en el reto anterior, también vimos como leer datos de JSON, consultando a través de APIs.

En ocasiones, los datos que buscamos no se encuentran en estos formatos tan cómodos, y tenemos que leerlos de fuentes que están diseñadas para humanos, no para nuestros scripts.

Esto pasa con las páginas web. Por debajo son un XML diseñado para que se renderice de una forma atractiva en nuestro navegador, no para facilidad de consulta. El diseño de aplicaciones que leen datos de webs se conoce como [web scraping](https://en.wikipedia.org/wiki/Web_scraping).

Gracias a esta técnica, podemos importar casi cualquier cosa que seamos capaz de visualizar a través de nuestro navegador. A veces con menos, a veces con más esfuerzo.

Pero también las webs, especialmente aquellas en las que su valor de negocio reside en sus datos, intentan protegerse frente a esta técnica. Si tienes curiosidad, puedes leer más sobre cómo se protegen [aquí](https://github.com/JonasCz/How-To-Prevent-Scraping).

## Scraping de datos metereológicos

Pongamos que necesitamos datos metereológicos de Madrid horarios del año 2008. Concretamente:

* Temperatura (ºC)
* Dirección del viento (si es N, SE, ...)
* Velocidad del viento (km/h)

Existen varias APIs para consultar datos metereólogicos, pero casi todas tienen alguno de los siguientes problema:

* De pago
* Limitaciones en número de llamadas
* No disponen de datos antiguos

Así que vamos a _scrapearlos_. Echa un vistazo a la siguiente página: http://www.ogimet.com/cgi-bin/gsynres?ord=REV&decoded=yes&ndays=31&ano=2008&mes=1&day=31&hora=24&ind=08221 .

Fíjate en los parámetros: están cuidadosamente elegidos, para obtener los datos horarios de todo enero de 2018. Aquí no hay documentación, ya que no está hecha para consulta de datos por script. Utiliza sentido común y juega cambiando los parámetros a mano hasta que sepas para qué funciona cada uno.

Tu objetivo es descargarte los datos horarios de todo 2008 de la estación `08221`, que es Barajas. Vamos a dividir esto en dos tareas más pequeñas para ir avanzando.

* Primero, crea una función que dado un año y un mes, te devuelva un dataframe con la fecha más hora, y los tres datos que queremos: temperatura (columna `T (C)`), dirección del viento (columna `ddd`) y velocidad del viento (columna `ff kmh`). Para la fecha con hora, puedes utilizar la estructura que más cómoda te sea: un objeto que contenga información detallada de tiempo, como `POSIX*t` en R o `datetime` en Python, o guardar por una parte la fecha (`Date` en R, `date` en Python) y por otra la hora (un entero). El resto de columnas deben tener también un tipo de dato adecuado: número con decimal para temperatura y velocidad, y cadena de caracteres para dirección del viento.

* Completa el script para que itere llamando a la función para todos los meses que necesitas extraer. El resultado final debe ser un único dataframe con los datos metereólogicos requeridos para todo el año 2008.

Puede que te encuentres con pequeños problemas que de primeras no sabes resolver, como por ejemplo:

* Extraer el número de días de un determinado mes
* Juntar la salida en un único dataframe
* Eliminar filas repetidas de un dataframe

Consulta en internet cómo resolverlo en concreto para el lenguaje que usas. Si te atascas, pregunta por el grupo de slack.

Sube la solución a tu repositorio de GitHub, en una carpeta `03_web_scraping` y llama al fichero `scrape_meteo.[R/py]`

## Anexo

A continuación detallo una serie de librerías y consejos que te pueden servir para resolver el problema, pero no deja de ser una recomendación. Si prefieres usar otras librerías, ¡adelante!

* R: el paquete `XML` trae una librería muy útil para este caso, `readHTMLTable`.
* Python: el propio `Pandas` tiene una función para leer tablas HTML, `read_html`. Documentación [aquí](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_html.html). Puede que necesites alguna librería extra para importar la tabla.

Esta página tiene una complicación extra: la web en sí está maquetada con tablas (una práctica muy habitual hace años). En R no he tenido problemas para leerlo. En cambio, en Python, si hago directamente `read_html` sobre la página, se queda pillado (al menos varios minutos, yo he tenido que matarlo). Un truco es, en lugar de decirle que intente parsear todas las tablas del html, es pasarle únicamente la tabla de interés. Lo puedes hacer:

* Descargando la página con `request.get`.
* Parseándola con `BeautifulSoup` (excelente librería para hacer web scraping en general).
* Y luego, diciéndole a `pandas.read_html` que solo lea esa tabla.

_Spoiler_: Intenta hacerlo tú mismo. Si te atascas, pongo más abajo la solución de este primer paso:

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.

.


```
import pandas as pd
import requests
from bs4 import BeautifulSoup

# Descarga del html
res = requests.get('http://www.ogimet.com/cgi-bin/gsynres?ord=REV&decoded=yes&ndays=31&ano=2008&mes=1&day=31&hora=24&ind=08221')

# Parseo
soup = BeautifulSoup(res.content, 'lxml')

# Busco la tercera tabla
table = soup.find_all('table')[2]

# Paso la tabla a pandas. Ademas, me quedo solo con las primeras columnas,
#  que es donde va a estar la informacion interesante
df = pd.read_html(str(table))[0].iloc[:,0:15]
df.head()
```

__Y cuidado__, como podrás ver la cabecera se ha desplazado con respecto a los datos.
