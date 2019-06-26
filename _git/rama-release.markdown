---
title: Rama Release
date: 2019-06-25 23:18:00 -04:00
position: 7
---

### Descripción

La rama “**release**” se debe utilizar para la preparación de una nueva entrega en el ambiente de producción. Esta rama es útil para corregir pequeños defectos y preparar los metadatos que deberá llevar la próxima entrega \(número de versión, fecha de compilación, etc.\). El beneficio de tener una rama de entrega **release** radica en el hecho de que podemos conservar la rama **develop** limpia y lista para recibir nuevas versiones que se tendrán que integrar a la rama **master**. Adicionalmente, la rama **release** será utilizada por el equipo de **QA** para probar la entrega antes de que esta llegue a producción.

### Rama de la que bifurca

`develop`

### Rama con la que se une

* `develop`
* `master`

### Convención de nombrado

El nombrado de esta rama se deberá de apegar a lo establecido en \[AGIS\] y la propuesta en esta sección:

Nomenclatura obligatoria: `release-*`

Ejemplo:

* `release-seguridad`
* `release-carrusel`

### Lineamientos

1. El mejor momento para crear una ramificación de develop es cuando el desarrollo refleja el estado deseado de una nueva entrega.

2. Todas las funcionalidades o características que se esperan mostrar en la próxima entrega deberán de unirse a la rama de develop.

3. Es exactamente al comienzo de la creación de esta rama en que se asigna una versión. Es hasta ese momento que la rama develop refleja los cambios para la siguiente entrega, pero no es claro si esa nueva entrega eventualmente se convertirá en la versión 0.3 o 1.0. La notación para el versionamiento de código es la descrita en [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html)

### Diagrama

![](/assets/images/git/branch-hotfixes.png)

### Comandos

Creación de la rama de entrega `release-1.2`

```bash
git checkout -b release-1.2 develop
```

Una vez que se a trabajo en la nueva rama, para actualizar los cambios en la rama develop primero tenemos que regresar a la rama develop y partir de allí llevar a cabo una unión \(merge\):

```bash
./bump-version.sh 1.2
```

Unir las modificaciones hechas en la rama feature dentro de la rama develop:

```bash
git commit -a -m "Bumped version number to 1.2"
```

Cambiarnos a la rama de master:

```bash
git checkout master
```

Unir los cambios de la rama release1.2 con master:

```bash
git merge –no-ff release-1.2
```

Enviar los cambios a la rama develop

```bash
git tag –a 1.2
```
