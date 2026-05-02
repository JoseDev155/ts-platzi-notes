# TypeScript vs. JavaScript

## JS vs TS

¿Qué debo tener en cuenta?

* ¿TypeScript != JavaScript?
* ¿TypeScript Dev != JavaScript Dev?

**JavaScript** ha tenido un incremento y su uso es exponencial, lo podemos utilizar en apllicaciones móviles, IoT, backend, frontend, etc.

Pero no fue creado como un lenguaje maduro desde el inicio, sino que fue a través del tiempo.

Pero a la hora de ejecutar código en JavaScript, con los errores:

>"Solo te das cuenta hasta que el código está en ejecución".

Así sea en un navegador, corriendo con Node.js en el backend, etc.

Como desarrolladores:

>"El objetivo es tener menos errores en producción y feedback rápido en desarrollo".

Hay vamos a tener en cuenta lo siguiente, porque al final lo que JavaScript toma como subset de JavaScript es todo lo que tenemos
actualmente de JavScript, más lo que se venga de JavaScript (tiene varias versiones, ES6, ES7, 2021, etc), muchas de esas caractrísticas no
están disponibles al instante; TypeScript toma esto, JavaScript y las versiones nuevas, y les pone **tipos**.
Vamos a tener un **análisis estático del código**.

Según el libro **Software Engineering at Google**, "entre más rápido encontremos un error, va a ser más rápido solucionarlo". Y ellos dividen
todo esto en unas capas, cada vez que nosotros podamos entregar código:

* **Capa 1 - Análisis de código estático**: Corre directamente en nuestro editor de código, en dónde detecta errores fácilmente, tipos, funciones no definidas, etc. Aquí es dónde nos vamos a centrar, porque TypeScript es muy fuerte haciendo análisis de código estático.
* **Capa 2 - Unit tests**: Hacemos pruebas de cómo debería funcionar una función.
* **Capa 3 - Integration tests**: Vemos como funciona todo en conjunto.
* **Capa 4 - Code review**: En equipos de ingeniería, tenemos que enviar esto y verificar si cumplimos con las reglas de ingeniería en nuestro equipo.

Resultado del equipo de ingeniería de **slack**:

>Después de adoptar el lenguaje, dejaron de preocuparse de las cosas raras que pasan en JavaScript y comenzaron a confiar en el análisis de código estático, o también conocido como **compilador**.

Entonces, ¿TypeScript != JavaScript?: Si, hay una diferencia pero no mucha.
Si tenemos conocimiento básico de JavaScript, fácilmente vamos a incurrir en esta capa del análisis de código estático.