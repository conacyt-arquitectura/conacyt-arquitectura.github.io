---
title: DTO
date: 2019-10-11 13:00:00 -06:00
position: 4
---

Para los DTO (y en general para los modelos) se utilizarán Interfaces para la definición y una clase con un constructor para su implementación:  
Los archivos llevarán el nombre ***[nombre]-dto.model.ts***  
 
Ejemplo:
  
  
***persona-fisica-dto.model.ts***
```javascript
export interface IPersonaFisicaDto {
  id?: number;
  cvu?: string;
  nombre?: string;
  rfc?: string;
  curp?: string;
  correo?: string;
  apellidoPaterno?: string;
  apellidoMaterno?: string;
  genero?: string;
}

export class PersonaFisicaDto implements IPersonaFisicaDto {
  constructor(
    public id?: number,
    public cvu?: string,
    public nombre?: string,
    public rfc?: string,
    public  curp?: string;
    public correo?: string,
    public apellidoPaterno?: string,
    public apellidoMaterno?: string,
    public genero?: string,
  ) {}
}

```  