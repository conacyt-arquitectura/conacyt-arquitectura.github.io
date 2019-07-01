---
title: Versionamiento (Ciclo)
date: 2019-06-25 23:18:00 -04:00
position: 10
---

Los lineamientos de versionamiento, se deberán de utilizar en momentos diferentes; dependiendo del tipo de proyecto, tamaño del equipo y el plan de iteración. De manera general, se identifican dos grandes fases que gobiernan a cualquier tipo de proyecto: **fase de inicio** y **fase de desarrollo**.

## Fase de  Inicio

### 1. inicialización

```bash
crearRama('from=empty', 'master')
```

#### individual

```bash
clonar(master)
version('0.0.1-SNAPSHOT', pom.xml )-commit-publish
```

### 2. flujo **increment** (arquitectura):

```bash
[update-]develop-commit[-publish]
```

### 3. flujo **release** (release-arquitectura):

#### 3.1 Inicialización

```bash
create('branch', 'release-arquitectura')
version('0.0.z-RC')-commit[-publish]
build('0.0.z-RC+dev#hash')
build('0.0.z-RC+qa#hash')
build('0.0.z-RC+prod#hash')
```

#### 3.1 SubFlujo Pruebas (release-arquitectura) :

```bash
foreach(enviroment = {'qa'})
    until enviroment is stable:
         test-report-solve-version('0.0.(z+1)-RC', pom.xml)-commit-publish]
          build('0.0.z-RC+enviroment #hash')
```

#### 3.2 SubFlujo Pruebas Finalización (release-arquitectura) :

```bash
version('0.0.z-RELEASE', pom.xml)-commit[-publish]
merge('release-arquitectura', 'master')-tag('0.0.z')
```

#### 3.3. Publicación

```bash
build('0.0.z-RELEASE+dev#hash')-publish(dev)
build('0.0.z-RELEASE+qa#hash')-publish(qa)
build('0.0.z-RELEASE+prod#hash')-publish(prod)
crearRama('from=master', 'develop')
version('0.0.z-SNAPSHOT', pom.xml)-commit[-publish]
publish('develop')
```

### 4. Terminación

#### individual

```bash
usarRama('develop')
```

---

# Fase de Desarrollo

## 1. Inicialización

```bash
crearRama(from='develop', 'feature-[nombre]')
version('0.(y+1).0-SNAPSHOT', pom.xml )-commit-publish
```

#### individual

```bash
clonar('feature-[nombre]')
```

### 2. Flujo increment (feature-[nombre]):

```bash
<ciclo>[update-]develop-commit[-publish]
```

## 3. Flujo Release (release-[nombre]):

#### 3.1 Inicialización

```bash
merge('feature-[nombre]', 'develop')-publish
crearRama('from=develop', 'release-[nombre]')
version('0.y.0-RC')-commit[-publish]
build('0.y.0-RC+dev#hash')
build('0.y.0-RC+qa#hash')
build('0.y.0-RC+prod#hash')
```

#### 3.2 SubFlujo Pruebas (release-[nombre]) :

```bash
<ciclo> test-report-solve-version('0.y.(z+1)-RC', pom.xml)-commit-publish]
```

#### 3.3 SubFlujo Pruebas Finalización (release-[nombre]) :

```bash
version('0.y.z-RELEASE', pom.xml)-commit[-publish]
merge('release-[nombre]', 'master')-tag('0.y.z')
```

#### 3.4 Publicar

```bash
merge('release-[nombre]', 'develop')-publish
build('0.y.z-RELEASE+dev#hash')-publish(dev)
build('0.y.z-RELEASE+qa#hash')-publish(qa)
build('0.y.z-RELEASE+prod#hash')-publish(prod)
eliminarRama('release-[nombre]')
```

preparar el siguiente incremento

```bash
version('0.y.z-SNAPSHOT', pom.xml)-commit[-publish]
publish('develop')
```

## 4. Terminación

#### individual

```bash
usarRama('develop')
```
