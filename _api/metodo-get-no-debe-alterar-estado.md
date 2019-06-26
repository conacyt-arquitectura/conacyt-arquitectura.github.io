---
title: El método GET no debe alterar el estado del recurso
date: 2019-06-26 13:05:46.559000000 -05:00
position: 2
---

Utillizar los métodos `PUT`, `POST` y `DELETE` en lugar del método `GET` para alterar el estado de un recurso.

Positive
: Usar:
```
PUT /usuario/711?activate
PUT /usuario/711/activate
```

Negative
: No Usar:
```
GET /users/711?activate
GET /usuario/711/activate
```
