---
title: Rama Hotfixes
date: 2019-06-25 23:18:00 -04:00
position: 8
---

## Rama Hotfixes

### Descripción

Una vez que se ha llevado a cabo una liberación a la rama `master` y esta versión forma parte del ambiente productivo del cliente, es posible que exista el reporte de nuevos `bugs` encontrados por los usuarios finales. Para corregir estos `bugs` y desplegar una nueva versión en el ambiente productivo, es que se utilizará la rama `hotfixe`, que ayudará a corregir errores que surgan en el ambiente de producción.

### Rama de la que bifurca

`master`

### Rama con la que se une

`master`
`develop`

### Convención de nombrado

hotfix-\[modulo-version\]

Ejemplo:

* `hotfix-seguridad-v1.1.1`
* `hotfix-carrusel-v1.1.1`

### Lineamientos

1. La rama `hotfixes` sólo existe mientras se está corriguiendo errores.
2. La rama `hotfixes` existe en el repositorio remoto.
3. La rama `hotfixes` es creada y eliminada por el rol master.
4. La operación **merge** con la rama `master` y la rama`develop` sólo la pude llevar a cabo el **rol master**.

Si existe una rama release cuando ocurre un bug en producción, entonces:

1. Los **bugs** corregidos en la rama `hotfix` se deberán de unir a la rama `release` y no a `develop`; la unión con `develop` ocurre cuando la rama `release` está lista para producción. Si el trabajo en la rama `develop` requiere de manera inmediata el cambio realizado en la rama `hotfix`, entonces se puede lleva a cabo la operación **merge** dentro de la rama `develop`;

### Diagrama

![](/assets/images/git/branch-hotfixes.png)

### Comandos

### Crear una rama `hotfix`

Las ramas hotfix son creados desde la rama master. Por ejemplo, si la versión que se liberó a producción fue la `1.2.0`, y se detectan errores durante el uso del sistema y los cambios en la rama `develop` no son estables, entonces se pude crear una rama `hotfix` para atender los bugs y volver a liberar a producción.

```bash
git checkout -b hotfix-1.2.1 master
./bum-version.sh 1.2.1
git commit -a -m "Versión modificada a 1.2.1"
```

Durante este paso se deberán de corregir los `bugs` en uno o varios `commits`:

```bash
git commit -m "Resolviendo bugs de producción"
```

Finalmente, se lleva a cabo un `merge` tanto a la rama `master` como a la rama `develop`,

Operación `merge` en la rama `master`:

```bash
git checkout master
git merge --no-ff hotfix-1.2.1
```

**Nota** Se puden utilizar las opciones`-s` o `-u` para firmar nuestro tag.

Operación `merge` en la rama `develop`:

```bash
git checkout develop
git merge --no-ff hotfix-1.2.1
```

**Nota** en caso que exista una rama de `release` los cambios en la rama `hotfix` deberán de unirse también en la rama `release`, en lugar de `develop`.

Eliminación de la rama temporal:

```bash
git branch -d hotfix-1.2.1
```
