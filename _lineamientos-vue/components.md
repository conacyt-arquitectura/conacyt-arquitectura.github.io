---
title: Components
date: 2019-10-11 13:00:00 -06:00
position: 2
---
  

Para el desarrollo de componentes, se deberán separar los archivos ***.vue*** y los ***.component.ts***  

Ejemplo: ***home.vue***
```vue
<template>
    <div class="home row">
  	<h1>{{mensaje}}</h1>
    </div>
</template>

<script lang="ts" src="./home.component.ts">
</script>

```  
  
***home.component.ts***
```javascript
import Component from 'vue-class-component';
import  Vue  from 'vue-property-decorator';

@Component
export default class Home extends Vue {
  public mensaje = “Este es un mesaje”;
}
```  