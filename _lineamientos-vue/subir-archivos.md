---
title: Subir Archivos con JhiDataUtils
date: 2019-11-05 13:00:00 -06:00
position: 7
---

Al trabajar con Jhipster, este nos provee de una clase llamada “JhiDataUtils” que contiene métodos que permiten trabajar con archivos. El uso básico se explica a continuación:  
  

El objetivo general es guardar un archivo como un objeto o como un atributo de un objeto, para ello se creará una clase que permita guardar el contenido del archivo y el tipo de contenido (para este ejemplo se usará el formato PDF):  
  
```javascript  
export interface IDocumento {
  id?: number; 
  contenido?: any; 
  contenidoContentType?: string; 
}

export class Documento implements IDocumento {
  constructor(
    public id?: number, 
    public contenido?: any,
    public contenidoContentType?: string
     ) { }
}
```   
***Nota:*** La libreria “JhiDataUtils” requiere que se le envíe un objeto con atributos donde guardar el contenido del archivo y el ContentType. Es necesario que el nombre del atributo en el que se guardará el ContentType del archivo tenga el mismo nombre que el atributo del objeto en el que se guardará el contenido seguido de "ContentType". Por ejemplo, si el atributo del objeto donde deseamos guardar el contenido de archivo se llama "information", deberá existir un atributo que se llame "informationContentType".  


Para cargar un archivo se utilizará un input desde el template:  
```vue
<input
      id="fileUpload"
      type="file"
      ref="fileUpload"
      accept="application/pdf"
      v-on:change="setFile($event)"/>

```  
Es a través del evento “change” que se podrá llamar al método con el que se guardará el archivo deseado.  
  
En el archivo de TypeScript deberá existir el método “setFile” y un objeto de tipo “Documento” que permita guardar el archivo que se cargará. Así mismo, el componente deberá heredar de la clase “JhiDataUtils” para hacer uso de uno de sus métodos llamado “setFileData”. El archivo quedaría de la siguiente manera:  
  
```javascript  
import JhiDataUtils from '@/shared/data/data-utils.service';
import { IDocumento, Documento } from '@/shared/model/documento.model';
import { mixins } from 'vue-class-component';
import { Component } from 'vue-property-decorator';

@Component
export default class GenericComponent extends mixins(JhiDataUtils) {
   public archivo: IDocumento;

   public setFile(event) {
       this.archivo = new Documento();
       this.setFileData(event, this.archivo, 'contenido', false);
   }
}

```  
  
El método “setFileData” de la librería “JhiDataUtils” asociará el archivo al objeto llamado “archivo”.  

Ahora también se podrá descargar ese archivo desde el template de la siguiente manera:  
```vue
<a class="pull-left" v-on:click="downloadDocument">
   <label>Documento</label>
</a>
```  
Y el método en el archivo TypeScript quedaría:  

```javascript
downloadDocument(){
   this.downloadFile(
        this.archivo.contenidoContentType,
        this.archivo.contenido,
        'nombreDocumento'
      );
}
```  
Quedando el componente de la siguiente manera:  
***generic-component.vue***  
```vue
<template>
  <div class="container">
    <input
      id="fileUpload"
      type="file"
      ref="fileUpload"
      accept="application/pdf"
      v-on:change="setFile($event)"/>
  </div>

  <a class="pull-left" v-on:click="downloadDocument">
     <label>Documento</label>
  </a>

</template>
<script lang="ts" src="./generic-component.component.ts">
</script>
```  
***generic-component.component.ts***  
```javascript  
import JhiDataUtils from '@/shared/data/data-utils.service';
import { IDocumento, Documento } from '@/shared/model/documento.model';
import { mixins } from 'vue-class-component';
import { Component } from 'vue-property-decorator';

@Component
export default class GenericComponent extends mixins(JhiDataUtils) {
   public archivo: IDocumento;

   public setFile(event) {
       this.archivo = new Documento();
       this.setFileData(event, this.archivo, 'contenido', false);
   }

   public  downloadDocument(){
      this.downloadFile( 	
            this.archivo.contenidoContentType, 
            this.archivo.contenido, 
            'nombreDocumento'
        );
  }
}
``` 




