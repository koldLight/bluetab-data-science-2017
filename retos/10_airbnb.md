# Reto inside AirBnB

El objetivo de este reto es proporcionar un análisis gráfico que identifique el uso que se hace de la plataforma Airbnb en Madrid o Barcelona. Es decir, que vayas explorando los datos y saques conclusiones apoyadas con gráficos en un notebook (Rmarkdown o notebook de jupyter).

Airbnb sostiene que su propósito es promover la economía de compartir. Es decir, que yo alquile mi casa mientras estoy de vacaciones en otro apartamento también ofrecido por una persona como yo, en el lugar que quiera visitar. Por el contrario, los negocios hoteleros se quejan de que realmente gran cantidad de los anfitriones en Airbnb hacen negocio con la plataforma, creando economía sumergida e incumpliendo medidas de seguridad, como la de exigir la identidad de los clientes.

Escoge Madrid o Barcelona (lo que prefieras) para hacer tu análisis. Los datos los puedes extraer de [Inside Airbnb](http://insideairbnb.com/get-the-data.html), que proporciona datasets _no oficiales_ sobre Airbnb en distintas ciudades. Los datos los obtienen mediante scraping de información pública en Airbnb.

## Organización del proyecto

Crea una carpeta en tu repositorio que se llame `10_airbnb` y crea tu notebook dentro. Descárgate los datos que necesites de [Inside Airbnb](http://insideairbnb.com/get-the-data.html) y guárdarlos en una carpeta `dat/`. Es probable que no necesites todos (el imprescindible es el de `listings`, pero hay datos sobre el calendario, un geojson de los barrios, ...), dependerá del análisis que quieras hacer.

## Los datos

Aunque los datos vienen bastante limpios, tendrás que hacer lo habitual, como conversión de tipos. Es recomendable que elimines los alojamientos que nunca se han alquilado, para no ensuciar el análisis (puedes suponer que si no tienen ninguna review, no se han alquilado aún).

## Sugerencias de gráficos

Este análisis es libre, puedes explorar y mostrar lo que prefieras. Lo que pongo aquí son solo sugerencias:

Como análisis básico:

* Muestra la cantidad de alojamientos por tipo (completo, habitación privada, habitación compartida)
* Muestra en un mapa los barrios coloreados por cantidad de alojamientos ofertados (p.e. gris las zonas con menos alojamientos, rojo intenso las que más)
* Muestra en un gráfico de [barras agrupadas](https://peltiertech.com/images/2011-07/CS_Col_00.png) los alojamientos por barrio y tipo.

Para analizar el uso de airbnb para hacer negocio:

* Crea una clasificación propia para intentar determinar el uso de cada alojamiento. Un criterio de clasificación de ejemplo:
    
    * Si el anfitrión solo tiene un alojamiento y lo tiene disponible menos de 90 días al año, podemos suponer que es alguien que lo alquila mientras está fuera durante sus vacaciones. Podemos clasificarlo como un alojamiento "vacacional".
    * Si el anfitrión solo tiene un alojamiento y es de tipo habitación privada, suponemos que son personas que alquilar una habitación de su propia casa mientras están ellos allí. Lo clasificamos como "habitación propia".
    * Si el anfitrión tiene varios alojamientos de tipo completo disponibles durante más de 90 días al año, suponemos que hacen negocio con la plataforma, alquilando de manera continua varios alojamientos. Lo clasificamos como "negocio".
    * Otros usos que no caigan en estos casos, pueden ser "otros". Si hay muchos de este tipo, conviene crear una división extra con el caso más mayoritario (p.e. anfitriones con un único alojamiento pero alquilado más de 90 días al año puede ser "segunda vivienda").

* Muestra la distribución de alojamientos por esta clasificación. Puedes introducir alguna variable más al gráfico que pueda ser interesante, como el barrio.
* Aproxima la ocupación mensual y lo que ingresa cada alojamiento con alguna heurística. Inside Airbnb comenta que:

    * El 50% de usuarios dejan una review tras el alquiler
    * La duración media del alquiler es de 3 noches, a no ser que el número mínimo de noches requerido sea superior
    * Los alojamientos suelen estar ocupados como máximo un 70% de los días que están disponibles

* Muestra la distribución de los ingresos mensuales en base a la clasificación que hemos hecho (negocio, vacacional, ...). Puede que tengas que jugar con diferentes escalas.
* Representa los barrios que están ingresando más dinero.
* Agrupa los alojamientos por ID de anfitrión, suma cuánto ingresa cada uno mensualmente por sus alojamientos, y represéntalo. Si observas una situación de desigualdad (unos pocos ingresan mucho), intenta resumirlo en una expresión del tipo el 10% de los anfitriones ingresan el 80% del total en la plataforma coherente con tus datos.
