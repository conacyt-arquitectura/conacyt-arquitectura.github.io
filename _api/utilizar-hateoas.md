---
title: HATEOS (Opcional)
date: 2019-06-26 13:05:46.559000000 -05:00
position: 6

---
HATEOAS (**H**ypermedia **a**s **t**he **E**ngine of **A**pplication **S**tate) deberá de ser utilizado para crear una mejor navegación a través del **API**

```json
{
  "id": 711,
  "manufacturer": "bmw",
  "model": "X5",
  "seats": 5,
  "drivers": [
   {
    "id": "23",
    "name": "Stefan Jauker",
    "links": [
     {
     "rel": "self",
     "href": "/api/v1/drivers/23"
    }
   ]
  }
 ]
}
```
