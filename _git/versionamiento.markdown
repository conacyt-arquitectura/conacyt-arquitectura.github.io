---
title: Versionamiento
date: 2019-06-25 23:18:00 -04:00
position: 9
---

La notación para **versionamiento** se ocupa en tres lugares: **(1)** Descriptor del Projecto _(ej. package.json, pom.xml)_, **(2)** Tag del commit que se está liberando _(ej. tag en commit the rama master)_, **(3)** Build del código fuente _(ej. .jar, .dll, etc)_
{: .note}

El estándar para versionamiento, está basado en [Semantic 2.0](https://semver.org/)

#### Lineamientos para versionamiento

1. Un número normal de versión **DEBE** tomar la forma `X.Y.Z` donde `X`, `Y`, y `Z` son enteros no negativos. `X` es la versión **“major”**, `Y` es la versión **“minor”**, y `Z` es la versión **“patch”**. Cada elemento **DEBE** incrementarse numéricamente en incrementos de 1. Por ejemplo: `1.9.0` -> `1.10.0` -> `1.11.0`

2. Una vez que un paquete versionado ha sido liberado **(release)**, los contenidos de esa versión **NO DEBEN** ser modificadas. Cualquier modificación **DEBE** ser liberada como una nueva versión

3. La versión `major` en cero `(0.y.z)` es para desarrollo inicial. Cualquier cosa puede cambiar en cualquier momento. El API pública no debiera ser considerada estable

4. La versión `1.0.0` define el API pública. La forma en que el número de versión es incrementado después de este release depende de esta API pública y de cómo esta cambia

5. La versión `patch` `Z` `(x.y.Z | x > 0)` **DEBE** incrementarse cuando se introducen solo arreglos compatibles con la versión anterior. Un arreglo de bug se define como un cambio interno que corrige un comportamiento erróneo

6. La versión `minor` `Y` `(x.Y.z | x > 0)` **DEBE** ser incrementada si se introduce nueva funcionalidad compatible con la versión anterior. Se **DEBE** incrementar si cualquier funcionalidad de la API es marcada como deprecada. **PUEDE** ser incrementada si se agrega funcionalidad o arreglos considerables al código privado. Puede incluir cambios de nivel `patch`. La versión `patch` **DEBE** ser reseteada a 0 cuando la versión `minor` es incrementada

7. La versión `major` `X` `(X.y.z | X > 0)` **DEBE** ser incrementada si cualquier cambio no compatible con la versión anterior es introducida a la API pública. **PUEDE** incluir cambios de nivel `minor` y/o `patch`. Las versiones `patch` y `minor` **DEBEN** ser reseteadas a 0 cuando se incrementa la versión `major`

8. Una versión `pre-release` **PUEDE** ser representada por adjuntar un guión y una serie de identificadores separados por puntos inmediatamente después de la versión `patch`. Los identificadores **DEBEN** consistir solo de caracteres **ASCII** alfanuméricos y el guión `[0-9A-Za-z-]`. Las versiones `pre-release` satisfacen pero tienen una menor precedencia que la versión normal asociada.Ejemplos: `1.0.0-alpha`, `1.0.0-alpha.1`, `1.0.0-0.3.7`, `1.0.0-x.7.z.92`

9. Los `meta-datos` del `build` **PUEDE** ser representada adjuntando un signo más y una serie de identificadores separados por puntos inmediatamente después de la versión `patch` o la `pre-release`. Los identificadores **DEBEN** consistir sólo de caracteres **ASCII** alfanuméricos y el guión `[0-9A-Za-z-]`. Los `meta-datos` del `build` **DEBIERAN** ser ignorados cuando se intenta determinar precedencia de versiones. Luego, dos paquetes con la misma versión pero distinta metadata de build se consideran la misma versión. Ejemplos: `1.0.0-alpha+001`, `1.0.0+20130313144700`, `1.0.0-beta+exp.sha.5114f85`

10. La precedencia se refiere a como son comparadas dos versiones una con la otra cuando son ordeandas. La precedencia **DEBE** ser calculada separando la _versión en major_, _minor_, _patch_ e identificadores `pre-release` en ese orden (La `meta-data` del `build` no figura en la precedencia). Las versiones `major`, `minor`, y `patch` son siempre comparadas numéricamente. La precedencia de `pre-release` **DEBE** ser determinada comparando cada identificador separado por puntos de la siguiente manera: los identificadores que solo consisten de números son comparados numéricamente y los identificadores con letras o guiones son comparados de acuerdo al orden establecido por **ASCII**. Los identificadores numéricos siempre tienen una precedencia menor que los no-numéricos. Ejemplo: `1.0.0-alpha` `<` `1.0.0-alpha.1` `<` `1.0.0-beta.2` `<` `1.0.0-beta.11` `<` `1.0.0-rc.1` `<` `1.0.0`
