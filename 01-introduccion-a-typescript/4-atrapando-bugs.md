# Clase 4 - Atrapando bugs

## Atrapando errores

Análisis estático de código

## Primer acercamiento a TypeScript

Nos vamos a `src/` y creamos un archivo `demo.js`. Dentro de el, copiamos el siguiente código JavaScript:

```javascript
(()=> {
  const myCart = [];
  const products = [];
  const limit = 2;

  async function getProducts() {
    const rta = await fetch('http://api.escuelajs.co/api/v1/products', {
      mehtod: 'GET'
    });
    const data = await rta.parseJson();
    products.concat(data);
  }
  function getTotal() {
    const total = 0;
    for (const i = 0; i < products.length(); i++) {
      total += products[i].prize;
    }
    return total;
  }
  function addProduct(index) {
    if (getTotal <= limit) {
      myCart.push(products[index]);
    }
  }

  await getProducts();
  addProducto(1);
  addProducto(2);
  const total = getTotal();
  console.log(total);
  const person = {
    name: 'Nicolas',
    lastName: 'Molina'
  }
  const rta = person +  limit;
  console.log(rta);
});
```

Aquí podremos ver unos errores, pero el editor/lenguaje no nos dice nada. Hasta que nosotros lo ejecutemos en un navegador o Node, vamos a
ver esos errores.

Pero lo que queremos es feedback temprano, ver el error mientras escribimos código.

Podemos activar el analizador de código estático de TypeScript, en archivos JavaScript.

Lo hacemos escribiendo en la primer línea del archivo:

```javascript
//@ts-check
```

Empezaremos a ver errores en todos lados. Por ejemplo, en JavaScript cuando llamamos a `fetch()`, tendremos un error de tipo ya que `mehtod`
no existe.

`rta.parseJson()` es un método que no existe. El método apropiado es `rta.json()`.

`length` va sin paréntesis `()`. En el caso de `i++`, al ser constante no puede cambiar; debería ser `let`.

En el caso de `await getProducts()`, `await` solo puede ejecutarse en una función que tenga `async`. Por lo que agregaremos a nuestra función clave:

```javascript
//@ts-check

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
    const total = 0;
    for (let i = 0; i < products.length; i++) {
      total += products[i].prize;
    }
    return total;
  }
  function addProduct(index) {
    if (getTotal <= limit) {
      myCart.push(products[index]);
    }
  }

  await getProducts();
  addProducto(1);
  addProducto(2);
  const total = getTotal();
  console.log(total);
  const person = {
    name: 'Nicolas',
    lastName: 'Molina'
  }
  const rta = person +  limit;
  console.log(rta);
});

```

Y podemos seguir puliendo este archivo JavaScript gracias a TypeScript para evitar errores peligrosos o que puedan salir en producción.

## Reto: Corregir todos los errores

Código corregido:

```javascript
//@ts-check

(async ()=> {
  const myCart = [];
  const products = /** @type {Array<{price: number}>} */ ([]);
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
  /**
   * @param {number} index
   */
  function addProduct(index) {
    if (getTotal() <= limit && Number.isInteger(index)) {
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
  const rta = `${person} ${limit}`;
  console.log(rta);
});
```