# Reto introducción programación

## 1. Cuenta y repositorio en GitHub

GitHub es un sitio web que ofrece repositorios git como un servicio. Es gratuito para repositorios públicos, pero también tiene planes de pago para proyectos privados. Gran parte del ecosistema open source usa GitHub como herramienta de colaboración.

Las soluciones a los ejercicios planteados durante este curso deberás subirlas a un repositorio público de tu propiedad. Para ello:

* Si aún no lo tienes, créate un perfil en [GitHub](https://github.com/)
* Después, [crea un repositorio](https://help.github.com/articles/create-a-repo/)

Un repositorio git nos sirve para gestionar cambios en nuestro código. Si es la primera vez que lo utilizas, ten en mente los siguientes conceptos básicos:

* Lo que tenemos en nuestro ordenador es el `working copy`.
* Lo que hay publicado en GitHub es el `remote`.
* Para subir nuestros cambios a GitHub, tenemos que hacer tres cosas:

    * Elegir los cambios a publicar.
    * Hacer commit, que marca todos los cambios elegidos como una nueva versión del código.
    * Hacer push, que publica el (o los) commits pendientes en el repositorio remoto.

Git se puede manejar de diferentes formas:

* Lanzando los comandos desde la terminal
* Utilizando una interfaz gráfica

Escoge con la que te sientas más cómodo. Si es la primera vez que lo usas, puede que prefieras la segunda opción. Buenas interfaces para git son:

* [SourceTree](https://www.sourcetreeapp.com) (recomendado): funciona en Mac y Windows
* [GitKraken](https://www.gitkraken.com): funciona en Mac, Windows y Linux
* [GitEye](https://www.collab.net/downloads/giteye): es portable, es decir, que no hace falta instalarlo. Buena alternativa si no tenéis permisos de administrador en la máquina que uséis.

## 2. Publica un .gitignore en tu repositorio

Vamos a publicar un primer cambio en nuestro repositorio: un fichero `.gitignore` en la raíz del proyecto. El contenido será el siguiente:

```
# History files
.Rhistory
.Rapp.history

# Session Data files
.RData
```

Si has instalado SourceTree, puedes seguir [este pequeño tutorial](http://www.bogotobogo.com/cplusplus/Git/Git_GitHub_Source_Tree_1_Commit_Push.php) para publicar tu primer cambio.

Este fichero sirve para ignorar los ficheros descritos en su interior. Es decir, para evitar subir ciertas cosas al repositorio. Pueden ser ficheros temporales como en este caso, contraseñas, configuración dependiente del entorno, etc. Para saber más sobre cómo ignorar ficheros puedes [leer esto](https://help.github.com/articles/ignoring-files/).

## 3. Múltiplos de 3 y 5

Empezamos con la programación. Resuelve el siguiente ejercicio con código:

> Si listamos todos los números naturales menores que 10 que son múltiplos de 3 o de 5, nos sale 3, 5, 6 y 9. La suma de ellos da 23.

> Encuentra la suma de todos los múltiplos de 3 o de 5 menores que 1000.

Para publicar el resultado, primero crea una carpeta llamada `01_intro_programacion`. Dentro de ella, mete tu solución en un fichero ejecutable, es decir `03_multiplos.R` o `03_multiplos.py`, dependiendo del lenguaje que escojas.

## 4. Suma de monedas

> En Inglaterra, existen monedas de penique y de libra (que son 100 peniques).
> Las monedas disponibles son: 1p, 2p, 5p, 10p, 20p, 50p, £1 (100p) y £2 (200p).
> Podemos sumar £2 de la siguiente forma: 1×£1 + 1×50p + 2×20p + 1×5p + 1×2p + 3×1p.

> ¿De cuántas formas distintas podemos sumar £2, usando cualquier cantidad de monedas?

Publica el resultado en la carpeta `01_intro_programacion`, en un fichero ejecutable `04_monedas.R` o `04_monedas.py`
