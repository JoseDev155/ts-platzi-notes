# Clase 5 - El compilador de TypeScript

## El compilador

Transpila TS y genera JS

Nuestro navegador, si estamos haciendo aplicaciones web, sólo lee archivos JavaScript, no va a reconocer archivos TypeScript. También va a
pasar lo mismo con Node, nativamente no se ejecutan archivos TypeScript.

TypeScript traduce todo el código a JavaScript. A este proceso lo llamaremos **transpilación**.

También lo podríamos ejecutar directamente en Node con la librería **ts-node**.

## Transpilación

Los archivos con extensión `.ts` de TypeScript, los vamos a pasar por un proceso de transpilación.

EL compilador de TypeScript, va a leer estos archivos y los va a traducir a JavaScript.

Ventajas:

* Con TypeSctript, tenemos análisis de código estático previniendo bugs.
* Seleccionar a que target vamos a mandar ese JavaScript que se va a traducir. Porque hay muchas versiones de JavaScript: ES3/ES5/ES6/2021.
* En ES3, no habían **arrow functions**, **await/async**, y muchas otras cosas que están en este momento en el ecosistema de JavaScript.

## Práctica

Vamos a `src/` y creamos nuestro primer archivo TypeScript, llamado `01-hello.ts`.

Escribimos:

```typescript
const myName = 'Nicolas';
console.log(myName);
```

En este momento, no estamos usando todas las bondades de TypeScript.

Ahora, vamos a pasarlo por el transpilador y generar el archivo JavaScript.

En la terminal, ejecutamos:

```bash
npx tsc src/01-hello.ts
```

* `tsc`: Compilador.
* `src/01-hello.ts`: `direccion/archivo.ts`.

Con esto, se habrá creado `01-hello.js`. El resultado es:

```javascript
var myName = 'Nicolas';
console.log(myName);
```

Ya que no estamos manejando un **scope** o un alcance de funciones, simplemente utilizó `var`.

Ahora, creamos una copia de `demo.js` pero con extensión `demo.ts`, y quitamos el `//@ts-check`, ya que no es necesario en archivos TypeScript.

Corregimos los errores que faltaban:

```typescript
(async ()=> {
  const myCart = [];
  const products = [];
  const limit = 2;

  async function getProducts() {
    const rta = await fetch('http://api.escuelajs.co/api/v1/products', {
      method: 'GET'
    });
    const data = await rta.json();
    products.concat(data);
  }
  function getTotal() {
    let total = 0;
    for (let i = 0; i < products.length; i++) {
      total += products[i].price;
    }
    return total;
  }
  function addProduct(index) {
    if (getTotal() <= limit) {
      myCart.push(products[index]);
    }
  }

  await getProducts();
  addProduct(1);
  addProduct(2);
  const total = getTotal();
  console.log(total);
  const person = {
    name: 'Nicolas',
    lastName: 'Molina'
  }
  // const rta = person + limit;
  // console.log(rta);
});
```

Si intentamos sumar un objeto con un número, JavaScript hará lo siguiente:

```javascript
const person = {
    name: 'Nicolas',
    lastName: 'Molina'
}
person + 1
// '[object Object]1'
```

Entonces, comentamos las últimas 2 líneas.

Podemos borrar `demo.js`. Y ahora, compilamos `demo.ts`:

```bash
npx tsc src/demo.ts
```

Tendremos algunos errores, ya que por defecto, TypeScript va a tratar de traducir esto a una versión muy vieja de JavaScript, exactamente ES3.
Donde cosas como `await`, `const`, no se pueden traducir. Necesitaríamos incluir algunas librerías si realmente queremos llevarlo a esa versión de
JavaScript.

Pero la versión soportada por todos los navegadores en este momento es ES5. ES6 está muy cerca de ser soportado por todos los navegadores.

Vamos a traducirlo a ES6:

```bash
npx tsc src/demo.ts --target es6
```

Ya no nos dará error. Resultado de `demos.js`:

```javascript
var __awaiter = (this && this.__awaiter) || function (thisArg, _arguments, P, generator) {
    function adopt(value) { return value instanceof P ? value : new P(function (resolve) { resolve(value); }); }
    return new (P || (P = Promise))(function (resolve, reject) {
        function fulfilled(value) { try { step(generator.next(value)); } catch (e) { reject(e); } }
        function rejected(value) { try { step(generator["throw"](value)); } catch (e) { reject(e); } }
        function step(result) { result.done ? resolve(result.value) : adopt(result.value).then(fulfilled, rejected); }
        step((generator = generator.apply(thisArg, _arguments || [])).next());
    });
};
(() => __awaiter(this, void 0, void 0, function* () {
    const myCart = [];
    const products = [];
    const limit = 2;
    function getProducts() {
        return __awaiter(this, void 0, void 0, function* () {
            const rta = yield fetch('http://api.escuelajs.co/api/v1/products', {
                method: 'GET'
            });
            const data = yield rta.json();
            products.concat(data);
        });
    }
    function getTotal() {
        let total = 0;
        for (let i = 0; i < products.length; i++) {
            total += products[i].price;
        }
        return total;
    }
    function addProduct(index) {
        if (getTotal() <= limit) {
            myCart.push(products[index]);
        }
    }
    yield getProducts();
    addProduct(1);
    addProduct(2);
    const total = getTotal();
    console.log(total);
    const person = {
        name: 'Nicolas',
        lastName: 'Molina'
    };
    // const rta = person + limit;
    // console.log(rta);
}));
```

Ahora, queremos que todo lo que salga como resultado de nuestro TypeScript, no lo deje en la misma carpeta `src/`. Que lo deje en una
carpeta aparte.

Normalmente a esa carpeta le vamos a llamar `dist/`, de **distribution**.

Para que el resultado lo mande a esta carpeta `dist/`, escribimos:

```bash
npx tsc src/demo.ts --target es6 --outDir dist
```

* `--outDir`: Carpeta de salida.

Aquí estamos transpilando archivo por archivo.

Pero, podemos usar una expresión regular para que tome todos los archivos que terminen en `.ts`, y los compile y los mande a esa carpeta:

```bash
npx tsc src/*.ts --target es6 --outDir dist
```

Ahora, borramos todos los archivos `.js` y mantenemos sólo archivos `.ts` en nuestro `src/`. Y los resultados de las transpilaciones en la
carpeta `dist/`.

Finalmente, una vez con los JavaScript transpilados por el compilador de TypeScript, ahora podemos ejecutarlo:

```bash
node dist/01-hello.js
```

Esto nos devolverá:

```plaintext
Nicolas
```

## Resumen

Proceso:

```bash
npx tsc src/hello.ts
node src/hello.js
# Node y browser just run JS
npx tsc src/hello.ts --outDir dist
npx tsc src/cart.ts --outDir dist
# By default target is ES3
npx tsc src/cart.ts --outDir dist --target es6
```

**Deno** es una tecnología creada por el mismo creador de Node en base a TypeScript. Y corre TypeScript por defecto, no hay que transpilarlo, es
TypeScript como lenguaje nativo de este entorno.

---

## Error al compilar todos los archivos TypeScript

El error:

```plaintext
error TS6053: File 'src/*.ts' not found.
  The file is in the program because:   
    Root file specified for compilation
```
Se resuelve creando un archivo `tsconfig.json`.

Pasos:

* Posicionarnos en el directorio raíz de nuestro proyecto.
* Ejecutar el comando `npx tsc --init`
  * Esto creará el archivo `tsconfig.json`
* Ejecutar el comando `npx tsc -p ./ -w`
  * Esto compilará en el mismo directorio todos los archivos `.ts`
* Modificar el `target` o el destino (para enviar los compilados a `/dist`) en el archivo `tsconfig.json` busca la bandera `"outDir"` y modifícala para que quede así: `"outDir": "./dist"`,
Listo, ya está configurado lo necesario para seguir el curso tal cual (hasta el momento).

* **Nota**: El tsconfig ya viene configurado para compilar a ES6, en caso de cambiarlo, buscamos la línea `"target"` y la modificamos con el valor que queramos.