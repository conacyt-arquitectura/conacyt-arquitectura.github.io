---
title: Router
date: 2019-10-11 13:00:00 -06:00
position: 3
---

Escribimos el archivo que contendrá las rutas, en cada objeto del arreglo Routes se define el path de la ruta, el nombre y el componente al que está referenciado.  
  
  

```javascript
import Vue from 'vue';
import Component from 'vue-class-component';
import Router from 'vue-router';

Component.registerHooks([
  'beforeRouteEnter',
  'beforeRouteLeave',
  'beforeRouteUpdate' // for vue-router 2.2+
]);

const Home = () => import('../core/home/home.vue');

Vue.use(Router);

export default new Router({
  mode: 'history',
  routes: [
    {
      path: '/',
      name: 'Home',
      component: Home
	meta: { authorities: ['ROLE_USER'] }
    }
  ]
});
```  