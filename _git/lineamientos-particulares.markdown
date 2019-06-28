---
title: Lineamientos Particulares
date: 2019-06-25 23:18:00 -04:00
position: 11
---

Los siguiente lineamientos aplican a todas la ramas:

* Tanto el nombre de los directorios, como el de los productos de trabajo que están contenidos en ellos no incluirán acentos, ni caracteres especiales, ni espacios.
* El código contenido en cualquier rama deberá ser versionado haciendo uso del juego de caracteres **UTF-8**.
* Salvo imágenes, las ramas sólo podrán contener código fuente. Ningún otro archivo de tipo binario deberá ser considerado para versionamiento en la rama de código. En caso que sea necesario subir imágenes, estas deberán de ser codificadas en **base64**.
* Efectuar el **push** sólo para las unidades funcionales completas.
* Efectuar **push** de manera frecuente. De ser posible, cada día, siempre y cuando esto no entre en conflicto con la regla anterior.
* Para **push** deberá generarse un comentario amplio y descriptivo que incluya el detalle de aquello que se está subiendo en el repositorio **Git**.
* Generar respaldos de la base de datos **Git** en una base mensual.
* No estará permitido efectuar bloqueos, a menos que esto sea justificado plenamente.

Los siguiente lineamientos deberá de ser considerados por los desarrolladores:

* Para comenzar a trabajar siempre hay que crear un branch a partir de origin develop.
* Probar el software antes de hacer un push al repositorio remoto **origin develp**.
* En caso que esté trabajando en una nueva funcionalidad y decides que no formará parte de la rama develop, entonces, para comenzar a trabajar sobre otra nueva funcionalidad siempre deberás de hacer un rebase a **develop**.
* Llevar a cabo la operación checkout a develop, para asegurarte que te encuentras trabajando con la última versión del proyecto en fase de desarrollo.
* Siempre prueba tu código una y otra vez.
* Los proyectos no deberán de ser creados por los integrantes del repositorio gitlab, únicamente el administrador será el único facultado en llevar a cabo este tipo de acciones.

