---
title: Configuración de cliente npm
date: 2019-07-23 13:00:00 -06:00
position: 6
---
En este documento se muestra cómo configurar el cliente npm para utilizar el/los repositorios npm privados de la organización

## Utilizar repositorio virtual en lugar de npm Registry
Esta es la manera más fácil de utilizar tanto las dependencias públicas (provenientes de **npm Registry**) y las dependencias privadas (de la organización). 
Configura el cliente npm para que utilice como *registry* el repositorio virtual (aquel que agrupa **npm Registry** y el repositorio npm privado).

    npm config set registry http://{SERVIDOR}/content/groups/npm/

## Utilizar repositorio privado solo para paquetes con `@scope`
También es posible utilizar el repositorio público de **npm Registry** para las dependencias públicas y el repositorio privado para descargar las dependencias de la organización siempre y cuando estas últimas utilicen *scope*s, por ejemplo `@conacyt/dependencia`. Para que el cliente npm instale dependencias de un *scope* específico desde un *registry* específico:

    npm config set @conacyt:registry http://{SERVIDOR}/content/groups/npm/

## Publicar paquete a un repositorio privado
Note que para publicar **no** se utiliza la URL del repositorio *virtual* o *agrupador* sino la URL del repositorio npm real.

Existen dos formas para publicar al repositorio privado. La primera consiste en especificar en el 
`package.json` la URL del registry donde se publicará el paquete.

    {
        ...,
        "publishConfig": {
            "registry": "http://{SERVIDOR}/content/repositories/npm-local/"
        }
    }

Para autenticarse agregue al archivo de configuración `~/.npmrc`las siguientes líneas:

    email=changeme@yourcompany.com
    always-auth=true
    _auth=YWRtaW46YWRtaW4xMjM=

La segunda forma consiste en especificar, además de la autenticación, el *registry* en el archivo de configuración `~/.npmrc` y **no** en el `package.json`. 

    email=changeme@yourcompany.com
    always-auth=true
    _auth=YWRtaW46YWRtaW4xMjM=
    @conacyt:registry=http://{SERVIDOR}/content/repositories/npm-local/

A continuación se publica el proyecto:

    npm publish

## Utilizando perfiles de configuración (Recomendado/La manera fácil)
Para evitar mezclar distintas configuraciones y lo recomendable es crear perfiles de configuración utilizando [npmrc](https://docs.npmjs.com/configuring-your-registry-settings-as-an-npm-enterprise-user).

De esta forma:
- Se puede alternar entre perfiles de configuración fácilmente con `npmrc {PERFIL}`
- El *registry* principal será el repositorio virtual
- Las dependencias con scope `@conacyt` se descargarán y publicarán en el repositorio npm privado  

```
# Instalando npmrc de manera global
npm i npmrc -g
# Creando un nuevo perfil con nombre 'conacyt'
npmrc -c conacyt
# Configurando el perfil para usar el registry privado virtual
npm config set registry http://{SERVIDOR}/content/groups/npm/
# Configurando el perfil para publicar los paquetes con scope '@conacyt' al repositorio npm privado
npm config set @conacyt:registry http://{SERVIDOR}/content/repositories/npm-local/
# Agregando autenticación al perfil
npm config set email changeme@yourcompany.com
npm config set always-auth true
# Codificando usuario y contraseña
echo -n 'usuario:contraseña' | openssl base64
# Copia y pega el resultado en el archivo de configuración de tu perfil como una nueva línea _auth=miUsuarioYContraseñaCodificados
vim ~/.npmrcs/conacyt
```