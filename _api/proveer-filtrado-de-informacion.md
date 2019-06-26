---
title: Filtrado de Información
date: 2019-06-26 13:05:46.559000000 -05:00
position: 7
---

Positive
: Proveer operaciones de filtrado (filtering),  ordenamiento (sorting), selección de campos (field selection) y Paginación (Paging) de colecciones

### Filtering

Utilizar sólo un parámetro de busqueda por cada campo que se desea filtrar:

```
GET /cars?color=red Regresa una lista de todos los carros Rojos
GET /cars?seats<=2 Regresa una lista de los carros que tienen un máximo de 2 asientos
```

### Sorting

Similar a `filtering`, en `Sorting` se utiliza un parámetro genérico llamdo **sort** que puede ser utilizado para describir reglas de ordenamiento; generalmente el ordenamiento es de tipo ascendente o descendente sobre varios campos separados por comas:

```shell
# Recupera los carros ordenamos de manera ascendente en el campo id
GET /cars?sort=id,asc

La consulta anterior regresará una lista de carros ordenados de manera ascendente en el campo id y de manera ascendente en el campo modelo.

# Recuepera todos los tickets en orden descendiente en el campo id.
GET /tickets?sort=id,desc
```

### Field Selection

Dar la posibilidad de elegir los campos que se desean regresar. Esto ayuda a reducir el tráfico en la red.

Ejemplo:

```
# Para la entidad Car
GET /cars?fields=manufacturer,model,id,color

# Para la entidad Tickets
GET /tickets?fields=id,subject,customer_name,updated_at&state=open&sort=-updated_at
```

### Paging

Utilizar la propiedad `page` y `size` para limitar el número de resultados que se desean recuperar.

Ejemplo:

```
GET /cars?page=0&size=5
```

Los links para las páginas siguientes, o previas, deberán de ser provista en el json que se regresa. Para la navegación a través del API deberá de ser a través de las siguientes propiedades:

```javascript
last : true o false
totalElements : Número de elementos en la base de datos
totalPages : Número de páginas que pueden mostrar para un determinado tamaño
first : true si el resultado es la primer página de la colección
numberOfElements : Número de elementos que se tiene en la página actual
sort : true Sí los valores están ordenados 
size : Tamaño de elementos que se muestran por ágina
number : Número de la página
```

Un ejemplo de la respuesta se muestra a continuación:

Solicitud:

```bash
curl -u dads:dads http://localhost:8080/rest-spring-jpa/dataStores?page=3\&size=2
```

Respuesta:

```javascript
{
  "content": [
    {
      "id": 1,
      "dataStoreType": {
        "id": 1,
        "name": "jdbc",
        "description": "Data Store for JDBC connector"
      },
      "url": "jdbc:mysql://localhost/membership?autoReconnect=true",
      "driverClass": "com.mysql.jdbc.Driver",
      "username": "developer",
      "password": "temporal123",
      "tableTypes": "TABLE,VIEW"
    }
  ],
  "last": true,
  "totalElements": 1,
  "totalPages": 1,
  "first": true,
  "numberOfElements": 1,
  "sort": null,
  "size": 1,
  "number": 0
}
```
