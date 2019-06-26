---
title: Rama Feature
date: 2019-06-25 23:18:00 -04:00
position: 5
---

### Descripción

La rama de características “**feature**” es utilizada para desarrollar nuevas características o funcionalidades que vendrán en las próximas o futuras entregas. Esta rama se crea cuando se comienza a desarrollar una nueva característica de la cual se desconoce la fecha de entrega. La esencia de esta rama es que exista durante el periodo de tiempo en que tome desarrollar la nueva característica. Eventualmente, esta rama se unirá a la rama de desarrollo **develop** \(para agregar de manera definitiva la nueva característica en la próxima entrega\) o se eliminará \(en caso de que la nueva característica no cumpla con los objetivos deseados\).

### Rama de la que bifurca

`develop`

### Rama con la que se une

`develop`

### Convención de nombrado

El nombrado de esta rama se deberá de apegar a lo establecido en \[AGIS\] y la propuesta en esta sección:

Nomenclatura Adicional:`feature-*`

Ejemplo:

* feature-seguridad
* feature-carrusel

### Lineamientos

1. Sólo existe en el repositorio local, nunca en el remoto **origin**

### Diagrama

![](/assets/images/git/branch-features.png)

### Comandos

Crear una rama `feature` a partir de la rama `develop` se deberá de hacer lo siguiente:

```bash
git checkout -b feature-seguridad develop
```

Una vez que se a trabajo en la nueva rama, para actualizar los cambios en la rama `develop` primero tenemos que regresar a la rama `develop` y partir de allí llevar a cabo la operación `merge`:

```bash
git checkout develop
```

Unir las modificaciones hechas en la rama `feature` dentro de la rama `develop`:

```bash
git merge --no-ff feature-seguridad
```

A continuación, se deberá de borrar la rama `feature-seguridad`:

```bash
git branch -d feature-seguridad
```

Finalmente, se envian los cambios a la rama remota `develop`

```bash
git push origin develop
```
