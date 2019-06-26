---
title: Notas Importantes
date: 2019-06-25 23:18:00 -04:00
position: 10
---

Existen dos cosas que nunca se deberá de llevar a cabo en **Git**:

1. **NUNCA** forzar una operación **push**: Si te encuentras en una situación donde tus cambios no puedas ser enviados al upstream, debido a que algo está mal.

2. **NUNCA** ejecutes la operación **rebase** a una rama a la que le has aplicado la operación **push** o **pull**. Esto puede generar la duplicidad de **_commits_** a un repositorio compartido.
