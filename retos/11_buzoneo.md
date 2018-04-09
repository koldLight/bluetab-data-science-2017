# Reto buzoneo

Estás trabajando en una empresa que organiza campañas de márketing. Varios clientes te piden que les organices una serie de campañas de buzoneo en Madrid, para las cuales tienen un público objetivo definido.

Tu trabajo las próximas TBA semanas será optimizar el esfuerzo dedicado. Es decir, intentar llegar al mayor número de personas de su objetivo dejando el menor número de folletos.

El buzoneo consiste en enviar a un repartidor de folletos a una serie de portales. El repartidor dejará un folleto en cada buzón, igual al número de viviendas existentes en tal portal.

## Las campañas

### Clases de español para chinos

La empresa __Ni hao España!__ ofrece un curso exprés de español a gente de procedencia china para aprender el idioma en 12 semanas. Su público objetivo es gente nacida en China.

### Gafas de sol

La empresa __Joquers__ ha creado unas nuevas gafas de sol modernas y low-cost. Su plan es conseguir que los estudiantes las lleven en las universidades en las que estudian y se extienda su compra por imitación. Su público son los estudiantes universitarios que están cursando actualmente estudios de grado.

### Móviles adaptados

Una empresa española de fabricación de teléfonos móviles acaba de lanzar el __Yayofón__. Se trata de un dispositivo que trae instalados tres botones de acceso rápido: uno al teléfono, otro al whatsapp y otro a la galería de fotos. La pantalla está adaptada para letras grandes y ofrecen un servicio gratuito de migración de agenda de contactos, historial de conversaciones y fotos del antiguo dispositivo al nuevo. Tenían claro que su público objetivo son los mayores de 65. Además, mediante un estudio de mercado, han descubierto que entre las mujeres tienen un grado de aceptación varios puntos por encima que entre los hombres.

### Transporte para ejecutivos

La empresa __Huver__ es competencia de los taxis en Madrid. Ofrecen un servicio de transporte con conductor a través de su aplicación móvil. Están actualmente lanzando una nueva línea de coches llamados __Sharknado X__ con servicios exclusivos para ejecutivos: coches lujosos con conectividad móvil asegurada (incluso en túneles), nevera con bebidas con alto contenido en cafeína y chófers con puntuación en conducción agresiva certificada de al menos 9 sobre 10. Definen a su público objetivo como hombres y mujeres con niveles de renta muy altos, con edades comprendidas entre los 35 y 50 años y con un nivel de estudios de diplomatura, licenciatura o máster.


## Hitos

### Estructura del proyecto

Tu proyecto deberá acabar teniendo esta estructura:

```
11_buzoneo/
  |-- dat/
    |-- raw/: carpeta que contiene los datos en crudo
    |-- sscc_madrid_data.csv: resultado de tratar raw/
  analisis.[Rmd|ipython]
``` 

### Creación del dataset

Examina el listado de enlaces en el apartado de Datos. Selecciona aquellos que vas a necesitar para poder segmentar la población y guárdalos en `dat/raw/`.

Crea una función que se llame `creaDataset` que lea los datos necesarios de `dat/raw`, los trate, los cruce y acabe generando el archivo `dat/sscc_madrid_data.csv`.

Es importante que este csv resultante sea cómodo de utilizar: nombres de columna intuitivos, nulos tratados, y los indicadores que van como filas o columnas bien elegidos. Te recomiendo que uses un formato que tenga una fila por cada sección censal, y los indicadores que necesites estén en columnas. Estos indicadores serán: número total de viviendas, número total de personas, número de personas nacidas en China, número de estudiantes de grado, etcétera.

### Ránking de secciones

Para cada campaña y sección, calcula lo siguiente:
- Total personas público objetivo
- Porcentaje de personas de la sección que son público objetivo
- Total folletos necesarios (que corresponde al total de viviendas de la sección)

Muestra el top 10 de las secciones más interesantes en las que buzonear (al menos en formato tabla, y de forma opcional, pintadas en un mapa). Una sección es más interesante cuanta más personas del público objetivo vivan ahí.

Ten en cuenta que en algunas campañas pueden tener indicadores mixtos que igual no puedes obtener en conjunto (p.e. tienes una columna `número personas con estudios universitarios` y otra `número de personas entre 35 y 50 años`). Para sacar el indicador combinado, es decir, que cumplan ambos requisitos, puedes suponer que son independientes y multiplica uno de ellos por el porcentaje de la población que cumplen el segundo. Siguiendo este ejemplo, si para una determinada sección, tenemos que:
- Total personas: 1000
- Núm personas con estudios universitarios: 200
- Núm personas entre 35 y 50 años: 250
- El resultado para calcular núm personas con estudios universitarios y que tengan entre 35 y 50 años sería: 200 * (250 / 1000) = 50

### (Opcional) Trayecto del buzoneador

Calcula la distancia mínima que tiene que recorrer el buzoneador para repartir los folletos en las 10 secciones que has elegido para cada campaña. Esto no es sencillo, deberás:

1. Generar una tabla que tenga la distancia entre cada sección censal (todas contra todas). Puedes utilizar la API de cartociudad con este fin (ver enlaces al final de este documento).
2. Resolver el [problema del viajante](https://en.wikipedia.org/wiki/Travelling_salesman_problem). Tanto en R como en Python, hay librerías que puedes usar para aplicar un algoritmo re resolución que devuelva la ruta óptima: busca por TSP en el lenguaje que necesites y úsalo
3. Calcula la distancia a recorrer en metros
4. Pinta la ruta en un mapa de leaflet

## Datos

Esta vez, tienes que fabricarte tu propio dataset. Estos enlaces pueden resultarte útiles:

- [Información resumida de población y hogares por secciones](http://www.ine.es/censos2011_datos/cen11_datos_resultados_seccen.htm)
- [Edad, sexo, país origen por secciones](http://www.ine.es/dynt3/inebase/es/index.htm?type=pcaxis&file=pcaxis&path=%2Ft20%2Fe245%2Fp07%2F%2Fa2017)
- [Nivel renta por secciones](http://www.madrid.es/portales/munimadrid/es/Inicio/El-Ayuntamiento/Estadistica/Areas-de-informacion-estadistica/Economia/Renta/Renta-neta-media-de-los-hogares-Urban-Audit-?vgnextfmt=default&vgnextoid=65e0c19a1666a510VgnVCM1000001d4a900aRCRD&vgnextchannel=ef863636b44b4210VgnVCM2000000c205a0aRCRD)
- [Consulta a medida del censo 2011](http://www.ine.es/censos2011/tablas/Inicio.do): tanto la creación como la tabla resultado son un poco feas. De aquí, los únicos datos que necesitas sacar son el número de personas por cada sección censal de Madrid que son actuales estudiantes de un grado universitario, intenta evitar usarlo para otros datos.

También he dejado en `dat/centroides_sscc_madrid.csv` las secciones censales de Madrid con sus centroides. Están calculados del [shapefile que provee el INE](http://www.ine.es/censos2011_datos/cen11_datos_resultados_seccen.htm) de las secciones censales de España usadas para el censo del 2011.

## Otros enlaces

- [Documentación de la API de cartociudad](http://www.cartociudad.es/recursos/Documentacion_tecnica/CARTOCIUDAD_ServiciosWeb.pdf): puedes mirar el método de la API `route` para calcular distancias entre dos puntos de la cartografía española
- [Mapas de leaflet en Python](http://python-visualization.github.io/folium/docs-v0.5.0/index.html)
- [Mapas de leaflet en R](https://rstudio.github.io/leaflet/)
