---
title: Consumo de API
date: 2019-10-11 13:00:00 -06:00
position: 5
---

Para el consumo de un API REST se deberá crear un archivo del tipo ***[nombre].service.ts***, el cual contendrá una clase con los respectivos métodos para consumir los servicios.  

Ejemplo:  




***persona-fisica.service.ts***
```javascript
import axios from 'axios';

import { IPersonaFisica } from '@/shared/model/persona-fisica-dto.model';

const baseApiUrl = 'api/persona-fisicas';

export default class PersonaFisicaService {

   //Aquí iran los métodos para consumir los servicios

}

```  

#### GET  
Para obtener un elemento:  
```javascript
public find(id: number): Promise<IPersonaFisica> {
    return new Promise<IPersonaFisica>(resolve => {
      axios.get(`${baseApiUrl}/${id}`).then(function(res) {
        resolve(res.data);
      });
    });
  }
```  
  
  
Para obtener todos los elementos:  
```javascript
 public retrieve(): Promise<any> {
    return new Promise<any>(resolve => {
      axios.get(baseApiUrl + `?`).then(function(res) {
        resolve(res);
      });
    });
  }
```  
  
#### DELETE   
```javascript
public delete(id: number): Promise<any> {
    return new Promise<any>(resolve => {
      axios.delete(`${baseApiUrl}/${id}`).then(function(res) {
        resolve(res);
      });
    });
  }
```  
  
#### POST  
Para crear un elemento
```javascript
public create(entity: IPersonaFisica): Promise<IPersonaFisica> {
    return new Promise<IPersonaFisica>(resolve => {
      axios.post(`${baseApiUrl}`, entity).then(function(res) {
        resolve(res.data);
      });
    });
  }
```  

#### PUT  
Para actualizar un elemento  
```javascript
public update(entity: IPersonaFisica): Promise<IPersonaFisica> {
    return new Promise<IPersonaFisica>(resolve => {
      axios.put(`${baseApiUrl}`, entity).then(function(res) {
        resolve(res.data);
      });
    });
  }
```  

  