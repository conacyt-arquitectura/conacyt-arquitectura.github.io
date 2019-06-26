---
title: Rama Master
date: 2019-06-25 23:18:00 -04:00
position: 3
---

### Descripción

La rama **master**, por convención, será la rama principal del proyecto. En esta rama se encuentran las versiones productivas del sistema y que se han liberado a producción.

### Rama de la que bifurca

`Ninguna`

### Rama con la que se une

`Ninguna`

### Convención de nombrado

Esta rama **siempre** se llama `master`

### Lineamientos

1. No está permitido subir “código roto” a la rama master.
2. El código que se suba a master deberá de ser cuidadosamente probado antes de ser integrado; se sugiere utilizar el branch _release_ antes de que una nueva liberación se lleve a cabo a la rama **master**.
3. Sólo el **rol master** puede ejecutar la operación de `push/merge` a esta rama.
4. Esta rama **nunca** se deberá de borrar.

### Diagrama

![](/assets/images/git/branch-develop.png)

### Comandos

`[NO APLICA]`
