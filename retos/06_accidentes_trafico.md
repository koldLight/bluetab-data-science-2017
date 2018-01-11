# Reto datos de accidentes de tráfico

Varios periódicos nacionales publicaban hace unas semanas [noticias como esta](http://www.eldiario.es/politica/DGT-accidentes-trafico_0_673683119.html) con el titular "La DGT se enfrenta al cuarto año consecutivo de aumento de muertes en las carreteras". También afirma:

> En 2014 se rompió la tendencia a la baja que comenzó diez años atrás, siendo 2016 el año más acusado.

La DGT tiene estos datos públicos [aquí](http://www.dgt.es/es/seguridad-vial/estadisticas-e-indicadores/accidentes-30dias/series-historicas/). Vamos a hacer un pequeño análisis sobre estos datos para intentar sacar algunas conclusiones.

## 1. Descarga de los datos y estructura del análisis

Los datos, se pueden bajar del link indicado. Descárgate el excel más reciente (el de 2016), que contiene datos desde 1993. Colócalo en una carpeta `dat/` en el directorio donde estás programando.

El código, escríbelo en un Rmarkdown o notebook de jupyter.

Una vez finalizado, publica el código en tu repositorio, con una estructura similar a:

```
06_accidentes_trafico/
  |-- dat/                  (carpeta con los datos)
  |-- analisis.[Rmd/ipynb]  (con el código)
  |-- analisis.html         (resultado de ejecutar el notebook)
```

## 2. Lectura de los datos

Lee del excel la hoja `M_I-U_Meses`. Quédate con las columnas del año y el total. Es conveniente que pongas nombres a las columnas más cómodos de manejar (todo en minúsculas y sin eñes).

## 3. Un gráfico

Pinta en un gráfico de líneas la evolución del total de fallecidos a lo largo de los años.

Escoge la herramienta que prefieras. Puedes usar plot (en R base) o ggplot (más avanzado), o matplotlib (en Python).

¿Qué puedes ver en el gráfico? ¿Han aumentado los fallecidos en los últimos años?

## 4. Otro planteamiento

Podríamos pensar que, efectivamente, han aumentado los fallecidos en los últimos años. Pero también podemos plantearnos si el análisis es el correcto. Cada año, hay más vehículos en circulación. Un aumento de los fallecidos podría ser simplemente porque hay más coches.

Cambiemos la métrica del análisis. En lugar de mirar el número total de fallecidos, vamos a mostrar la evolución del número de fallecidos por cada millón de vehículos.

Hay datos sobre la cantidad de vehículos [aquí](http://www.dgt.es/es/seguridad-vial/estadisticas-e-indicadores/parque-vehiculos/series-historicas/). Descárgate el excel de 2016 y colócalo en la carpeta `dat/`.

Lee del excel la hoja `parque_tipos`. Quédate con las columnas del año y el total. Una vez hecho, cruza los datos por año con los datos de fallecidos, de forma que tengas en el mismo dataframe el año, el número de fallecidos y el número de vehículos.

Ahora, calcula en una nueva columna el nuevo indicador: el ratio de fallecidos por cada millón de vehículos.

Sobre estos datos, fíjate en los últimos años. En la noticia, afirmaban que el número de fallecidos no paraba de crecer desde 2014. ¿Qué pasa con el ratio?

Vuelve a pintar el gráfico, pero presentando la evolución del ratio a lo largo de los años.
