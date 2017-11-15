# Reto consulta de APIs

En proyectos relacionados con datos, podemos tener diversas fuentes de datos: ficheros, bases de datos, imágenes, ... Una de ellas son las APIs, servicios web públicos o privados a los que podemos hacer peticiones y recoger la respuesta de manera *programada*.

También podemos hacer uso de APIs que ofrecen servicios. P.e., de análisis de sentimiento, de almacenamiento de datos o de geocodificación.

Y, otro uso muy habitual, es que realicemos una aplicación cuya interfaz de consulta sea una API diseñada por nosotros mismos. P.e. si realizamos un proyecto de detección de fraude y proporcionamos a nuestro cliente una API para consultar la predicción sobre nuevos datos, para re-entrenar el modelo o extraer métricas.

Para consultar una API, en general, necesitamos conocer lo siguiente:

* La URL a consultar
* El verbo a usar. Los más habituales son GET y POST, pero hay más: PUT, DELETE, ...
* Los parámetros de la consulta. Pueden ir en la propia URL (lo más habitual en las peticiones GET) o en el cuerpo de la petición (para POST) con diferentes formatos (clave-valor, JSON, ...)
* El formato de la respuesta: si viene en JSON / XML / otro y además la estructura de ésta.

Todo esto suele estar documentado.

Los ejercicios propuestos aquí deberás publicarlos en tu repositorio de GitHub del curso, en una carpeta nueva llamada `02_consulta_apis`

## 1. Introducción APIs

En el código base de R y Python vienen utilidades para consultar APIs, pero suelen ser más cómodas de utilizar las librerías especializadas:

* En R, `httr`. La documentación [aquí](https://cran.r-project.org/web/packages/httr/httr.pdf).
* En Python, `requests`. La documentación [aquí](http://docs.python-requests.org/en/master/).

Instala la librería correspondiente en tu entorno. En R, tendrás que usar `install.packages` y en Python, `pip` o `conda`.

Consulta la documentación y haz la siguiente petición:

* URL: `http://www.cartociudad.es/services/api/geocoder/reverseGeocode`
* Verbo: `GET`
* Parámetros: `lat=36.9003409` y `lon=-3.4244838`

De la respuesta, imprime:

* El cuerpo
* El código HTTP de estado
* Las cabeceras

La respuesta a este ejercicio debe llamarse `01_intro_apis.[R/py]`

## 2. Crímenes en Londres

Con la documentación de las dos APIs que vas a utilizar:

* Nominatim, de geocodificación, [aquí](http://wiki.openstreetmap.org/wiki/Nominatim)
* La policía de UK, con resultados de crímenes, [aquí](https://data.police.uk/docs/method/crimes-at-location/)

Haz lo siguiente:

* Pregunta a la API de Nominatim de a dónde (calle, ciudad, ...) pertenecen estas coordenadas: 51.4965946,-0.1436476
* Pregunta a la API de la policía de UK por crímenes cometidos cerca de esa localización en Abril de 2017
* A partir de la respuesta, haz un conteo de los crímenes que ha habido por cada categoría

La respuesta a este ejercicio debe llamarse `02_crimenes.[R/py]`
