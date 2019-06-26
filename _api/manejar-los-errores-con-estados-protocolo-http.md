---
title: Manejo de Errores
date: 2019-06-26 13:05:46.559000000 -05:00
position: 9
---

El estándar HTTP provee al rededor de 70 códigos para estados que describen los valores que regresan.

```javascript
200 – OK – Eyerything is working
201 – OK – New resource has been created
204 – OK – The resource was successfully deleted

304 – Not Modified – The client can use cached data

400 – Bad Request – The request was invalid or cannot be served. The exact error should be explained in the error payload. E.g. „The JSON is not valid“
401 – Unauthorized – The request requires an user authentication
403 – Forbidden – The server understood the request, but is refusing it or the access is not allowed.
404 – Not found – There is no resource behind the URI.
422 – Unprocessable Entity – Should be used if the server cannot process the enitity, e.g. if an image cannot be formatted or mandatory fields are missing in the payload.

500 – Internal Server Error – API developers should avoid this error. If an error occurs in the global catch blog, the stracktrace should be logged and not returned as response.
```

Se tiene que considerar el [payload](http://softwareengineering.stackexchange.com/questions/158603/what-does-the-term-payload-mean-in-programming) que se tiene que pagar para manejar de manera adecuada los mensajes anteriores en una respuesta json. Por ejemplo, el cliente del `API` deberá de saber como manejar una respuesta como la siguiete:

```javascript
{
  "errors": [
   {
    "userMessage": "Disculpa, el recurso solicitado no existe",
    "internalMessage": "El usuario no existe en la base de datos",
    "code": 34,
    "more info": "http://dads.infotec.mx/app/api/v1/errors/12345"
   }
  ]
}
```
