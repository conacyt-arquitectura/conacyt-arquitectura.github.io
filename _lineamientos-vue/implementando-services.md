---
title: Utilización de los métodos de las clases service
date: 2019-10-11 13:00:00 -06:00
position: 6
---
Para poder utilizar las clases de tipo service, se deben registrar en el archivo ***main.ts***  
  
```javascript  
//...
new Vue({
  el: '#app',
  components: { App },
  template: '<App/>',
  router,
  provide: {
    personaFisicaService: () => new PersonaFisicaService(),
    
  },
  i18n,
  store
});
//...
```

Las clases de tipo service se pueden implementar inyectándolas de la siguiente manera:  
  

```javascript
import { Component, Vue, Inject } from 'vue-property-decorator';

import { IPersonaFisica } from '@/shared/model/persona-fisica.model';
import PersonaFisicaService from './persona-fisica.service';

@Component
export default class PersonaFisicaDetails extends Vue {
  @Inject('personaFisicaService') private personaFisicaService: () => PersonaFisicaService;
  public personaFisica: IPersonaFisica = {};

  beforeRouteEnter(to, from, next) {
    next(vm => {
      if (to.params.personaFisicaId) {
        vm.retrievePersonaFisica(to.params.personaFisicaId);
      }
    });
  }

  public retrievePersonaFisica(personaFisicaId) {
    this.personaFisicaService()
      .find(personaFisicaId)
      .then(res => {
        this.personaFisica = res;
      });
  }

```  