# Clase 6 - Veamos el TSConfig.json

## TSConfig.json

Ahorra trabajo

Para no transpilar archivo por archivo, y decir el target, TyeScript nos da un archivo de configuración para nuestro proyecto, el `tsconfig.json`.

### Crear el `tsconfig.json`

En la terminal, ejecutamos:

```bash
npx tsc --init
```

* `tsc`: Es el compilador de TypeScript.

El archivo se verá así (pero con muchas opciones comentadas):

```json
{
  "compilerOptions": {
    "target": "es2016", // Especifica la versión de JavaScript a la que se va a transpilar el código TypeScript.
    "module": "commonjs", // Especifica el sistema de módulos que se va a utilizar en el código JavaScript generado.
    "strict": true, // Habilita todas las opciones de verificación estricta, lo que ayuda a detectar errores potenciales en el código.
    "esModuleInterop": true, // Permite la interoperabilidad entre módulos CommonJS y ES Modules.
    "skipLibCheck": true, // Omite la verificación de tipos en los archivos de declaración de las bibliotecas.
    "forceConsistentCasingInFileNames": true // Asegura que los nombres de archivo sean consistentes en cuanto a mayúsculas y minúsculas.
  }
}
```

Habilitamos `outDir`, `rootDir`:

```json
{
  "compilerOptions": {
    "outDir": "./dist", // Especifica el directorio de salida (compilado) para los archivos JavaScript generados.
    "rootDir": "./src" // Especifica el directorio raíz para los archivos TypeScript.
  }
}
```

Ahora, vamos a la terminal:

```bash
npx tsc
```

>Esto compilará todos los archivos TypeScript dentro de la carpeta `src` y los colocará en la carpeta `dist`, siguiendo la estructura de directorios.

### Creando otro archivo

Creamos un nuevo archivo llamado `02-demo2.ts`:

```typescript
const numbers = [1,3,4];
```

Volvemos a la terminal y ejecutamos:

```bash
npx tsc
```

Los archivos se compilarán aunque tenga errores, con:

```js
"use strict"; // Nativo de JavaScript
```

Las alertas que vimos en la terminal, ahora `demo.ts` tendrá esas alertas en las líneas correspondientes.

Ahora, vamos a ejecutar:

```bash
npx tsc --watch
```

* `--watch`: Constantemente va a estar leyendo los archivos TypeScript y haciendo la transpilación automáticamente. Con esto, no vamos a estar ejecutando el comando cada vez que hagamos un cambio.

Para probarlo, nos vamos a `02-demo2.ts` y paralelamente, abrimos `02-demo2.js` y vamos a ir viendo los cambios que se van haciendo en el archivo JavaScript cada vez que guardamos el archivo TypeScript:

```typescript
const numbers = [1,3,4];
console.log(numbers);
console.log(numbers);
```

```js
"use strict";
const numbers = [1, 3, 4];
console.log(numbers);
console.log(numbers);
```

### Resumen

Código TypeScript -> Transpilación a un target de JavaScript específico -> Código JavaScript.

Comandos vistos:

```bash
npx tsc --init  # Crea el archivo tsconfig.json
npx tsc         # Transpila el código TypeScript a JavaScript
npx tsc --watch # Compila los cambios de forma reactiva
```

Muchos proyectos (frameworks) tienen su propio `tsconfig.json`, por eso trabajamos con TypeScript de forma local.