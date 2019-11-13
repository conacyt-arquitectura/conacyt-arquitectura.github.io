---
title: Generador de Componentes VueJS en Typescript
date: 2019-11-13 17:08:00 -05:00
position: 4
---
> Un generador [Yeoman](https://yeoman.io/) de un nuevo componente para VueJS en Typescript

## Instalación
Se asume que ya se tiene instalado [NodeJS](https://nodejs.org/).  
Primero, usa el _registry_ de CONACYT.
```bash
npm config set registry https://artifacts.ccd.conacyt.mx/content/groups/npm/
```

Luego, instala [Yeoman](http://yeoman.io) y el `generator-vuejs-typescript-component` usando [npm](https://www.npmjs.com/).

```bash
npm install -g yo
npm install -g generator-vuejs-typescript-component
```

## Uso
Genera tu nuevo proyecto:

```bash
yo vuejs-typescript-component
```

## Proyecto generado
```
├── babel.config.js         # Configuración de Babel
├── bili.config.ts          # Configuración de Bili (un bundler)
├── example                 # Un ejemplo de uso del componente
│   ├── App.vue
│   ├── main.ts
│   ├── shims-tsx.d.ts
│   └── shims-vue.d.ts
├── package.json
├── README.md
├── src                     # El código fuente
│   ├── foo.component.ts    # El componente en Typescript
│   ├── foo.component.vue   # El componente de Vue
│   ├── index.ts            # Exporta el componente y la función install
│   ├── shims-tsx.d.ts
│   └── shims-vue.d.ts
└── tsconfig.json           # La configuración de Typescript
```