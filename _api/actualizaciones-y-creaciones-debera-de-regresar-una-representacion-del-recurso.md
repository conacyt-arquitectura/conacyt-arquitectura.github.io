---
title: La Actualización y Creación de un recurso siempre deberán de regresar información sobre la operación
date: 2019-06-26 13:05:46.559000000 -05:00
position: 11
---

Los métodos `PUT`, `POST` o `PATCH` pueden llevar a cabo modificaciones a los campos de un recurso, por lo tanto deberán de indicar, como parte de la respuesta, sí la operación fue de actualización (updated) o creación (created).

En el caso de una petición `POST` que resulte en una creación, se deberá de utilizar el `HTTP 201 status code` e incluir un `Location Header` que contenga una URL con el nuevo recurso.
