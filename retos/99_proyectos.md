# Proyecto final

El proyecto final consiste en hacer un análisis de la evolución de las multas de Madrid capital a lo largo del tiempo.

El dataset está [aquí](https://datos.madrid.es/portal/site/egob/menuitem.c05c1f754a33a9fbe4b2e4b284f1a5a0/?vgnextoid=fb9a498a6bdb9410VgnVCM1000000b205a0aRCRD&vgnextchannel=374512b9ace9f310VgnVCM100000171f5a0aRCRD&vgnextfmt=default)

## Objetivos

Aunque los objetivos se irán modificando según el avance, irán por aquí:

* Exploración de la base de datos, que conozcamos bien quién hace las denuncias (SER, policía, ...), qué volumetría hay, cuáles son las multas más habituales, cuáles están geolocalizadas, ...
* Estudiar la estacionalidad y tendencia de algunos tipos de multa. Se puede observar estacionalidad anual y semanal.
* Búsqueda de outliers sobre la serie temporal y, si se puede, encontrar justificación
* Búsqueda de cambios bruscos en tendencia y, si se puede, encontrar justificación. Para esto, podemos usar CasualImpact.
* Estudiar la evolución de denuncia de multas ante instalación de nuevos dispositivos como radares o cámaras de foto-rojo.
* Predicción de cantidad de dinero recaudado un día concreto
* Creación de un portal en Shiny para explorar multas, filtrando por varios selectores (tipo multa, denunciante, rango temporal, ...).
* Presentar el resultado del estudio a la datatón de datos abiertos en Madrid, que se lleva celebrando un par de años alrededor de septiembre.
