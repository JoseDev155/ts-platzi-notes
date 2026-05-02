# Clase 3 - Configurado nuestro proyecto

## Proyecto

Preparando nuestro entorno de trabajo

## Instalarlo

No lo vamos a hacer de forma global, vamos a instalar TypeScript sólo para el proyecto. Así normalemnte lo trabajamos en el mundo real.

Vamos a crear una carpeta, y dentro de ella vamos a instalar TypeScript como una dependencia de desarrollo:

```bash
npm install typescript --save-dev
npx tsc --version
```

Vamos a crear una carpeta:

```bash
mkdir ts-project
```

Dentro de esa carpeta, vamos a tener las configuraciones por defecto básicas como:

* `.gitignore`
* Configuración de nuestro editor

Abrimos VS Code:

```bash
cd ts-project
code .
```

Creamos nuestro primer archivo: `.gitignore`.

## `.gitignore`

Para tener un buen `.gitignore`, tenemos la página de [ gitignore.io](https://www.toptal.com/developers/gitignore).

Escogemos:

```plaintext
Windows macOS Linux Node
```

Le damos a **Create**. Y copiamos el contenido en un archivo llamado `.gitignore` en nuestro proyecto.

Otro de los archivos que vamos a manejar es el `.editorconfig`.

## `.editorconfig`

Nos ayuda a tener una configuración simple y sencilla a la hora de ejecutar código.

* **NOTA**: Quedará como parte de los recursos de está clase.

```conf
# Editor configuration, see https://editorconfig.org
root = true

[*]
charset = utf-8
indent_style = space
indent_size = 2
insert_final_newline = true
trim_trailing_whitespace = true

[*.ts]
quote_type = single

[*.md]
max_line_length = off
trim_trailing_whitespace = false
```

Para que está configuración funcione, vamos a tener que instalar la extensión:

* **EditorConfig for VS Code** de EditorConfig.

Luego, vamos a tener una carpeta que es `src/`.

## `src/`

Es donde vamos a estar trabajando la mayor parte de el tiempo, que es **source**, la fuente del código.

## Dependencias

Lo vamos a hacer desde la terminal:

```bash
npm init -y
```

Ahora tenemos un `package.json` con una configuración sencilla.

Ahora vamos a instalar la primer dependencia que necesitamos, TypeScript:

```bash
npm install typescript --save-dev
```

* `--save-dev`: Con esto indicamos que lo guarde como una dependencia de desarrollo.

TypeScript no lo lee ni Node nativamente ni el navegador, lo vamos a utilizar más en entorno de desarrollo.
Lo que va a leer al final el que lo ejecuta son archivos JavaScript.

Como no lo hemos instalado de manera global, comprobamos que se instaló de manera correcta y la versión:

```bash
npx tsc --version
```

* `npx`: Nos permite ejecutar una serie de librerías que sólo están dentro de este proyecto, no de manera global.
* `tsc`: TypeScript.