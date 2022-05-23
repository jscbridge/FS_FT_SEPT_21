![logotipo de The Bridge](https://user-images.githubusercontent.com/27650532/77754601-e8365180-702b-11ea-8bed-5bc14a43f869.png  "logotipo de The Bridge")


# [Bootcamp Web Developer Full Stack](https://www.thebridge.tech/bootcamps/bootcamp-fullstack-developer/)
### JS, ES6, Node.js, Frontend, Backend, Express, React, MERN, testing, DevOps

## Clase 4

**Promesas**
Una Promise (promesa en castellano) es un objeto que representa la terminación o el fracaso de una operación asíncrona. Una promesa representa un valor que puede estar disponible ahora, en el futuro, o nunca.

Una Promesa se encuentra en uno de los siguientes estados:

- pendiente (pending): estado inicial, no cumplida o rechazada.
- cumplida (fulfilled): significa que la operación se completó satisfactoriamente.
- arreglada (settled): se ha cumplido o se ha rechazado (resuelta).
- rechazada (rejected): significa que la operación falló.

Como los métodos `Promise.prototype.then()` y `Promise.prototype.catch()` retornan promesas, éstas pueden ser encadenadas.


![promise](../../assets/js_avanzado/clase4/promises.png)


- [MDN | Usar_promesas](https://developer.mozilla.org/es/docs/Web/JavaScript/Guide/Usar_promesas)
- [MDN | Promise ](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Promise)
- [promesas](https://lenguajejs.com/javascript/asincronia/promesas/)
- [promise-basics](https://javascript.info/promise-basics)
- [w3schools - js_promise](https://www.w3schools.com/js/js_promise.asp)
 -[ES6-for-humans | spanish-version](https://github.com/metagrover/ES6-for-humans/tree/spanish-version)

Mi primera promesa:
```javascript
let myPromise = new Promise(function(resolve, reject) {
  setTimeout(function() {
    resolve('Te saludo tras 3 segundos!! ');
  }, 3000);
});

myPromise.then(function(value) {
  console.log(value);
});

console.log(myPromise);
```

- Una promesa
```javascript
let contador = 0;
let error = false;
function testPromesa() {

    let numPromesaActual = contador++;

    console.log("Promesa nº ("+numPromesaActual+") - Iniciada")

    let miPromesa = new Promise(
    function(resolve, reject) {       

        console.info("Promesa nº("+numPromesaActual+") - Proceso asincrónico empezado");

        if(error){
            reject(numPromesaActual)
        } else{
        window.setTimeout(
            function() {
            resolve(numPromesaActual)
            }, Math.random() * 2000 + 1000);
        }
    });
    miPromesa.then(
    function(val) {
        console.info("Promesa nº ("+val+") - Proceso asincrónico terminado");
        console.warn("Promesa nº ("+numPromesaActual+") - Finalizada");
    }).catch(
        function(val){
        console.error("Promesa nº("+val+") - ERROR!!!");
    });
};

testPromesa();
```

```javascript
const guardaAleatorios = (iterations) => new Promise((resolve, reject) => {
  const numbers = [];
  for (let i = 0; i < iterations; i++) {
    const number = 1 + Math.floor(Math.random() * 6);
    numbers.push(number);
    if (number === 6) {
      reject({
        error: true,
        message: "Se ha sacado un 6"
      });
    }
  }
  resolve({
    error: false,
    value: numbers
  });
});
guardaAleatorios(10)
  .then(result => console.log("Tiradas correctas: ", result.value))
  .catch(err => console.error("Se ha sacado un ", err.message));
```

- **.race()**

```javascript   
    let p1 = new Promise(function(resolve, reject) {
        setTimeout(resolve, 400, "Promesa 1");
    });
    let p2 = new Promise(function(resolve, reject) {
        setTimeout(resolve, 200, "Promesa 2");
    });

    Promise.race([p1, p2]).then(function(value) {
      console.log(value); // "segunda" - Promesa 2 más rápida
    });
```
- **.all()**
```javascript
    let error = false

    let p1 = new Promise(function(resolve, reject) {
      console.log("Promesa 1 - Iniciada");
      setTimeout(resolve, 1100, "Promesa 1 - Terminada");
    });
    let p2 = new Promise(function(resolve, reject) {
      console.log("Promesa 2 - Iniciada");
      setTimeout(resolve, 1800, "Promesa 2 - Terminada");
    });
    let p3 = new Promise(function(resolve, reject) {
      if(error){
        reject("modo error Activado");
      } else {
        console.log("Promesa 3 - Iniciada");
        setTimeout(resolve, 2900, "Promesa 3 - Terminada");
      }

    });
    let p4 = new Promise(function(resolve, reject) {
      console.log("Promesa 4 - Iniciada");
      setTimeout(resolve, 5100, "Promesa 4 - Terminada");
    });

    Promise.all([p1, p2, p3, p4]).then(function(value) {
      console.info("Promise.all -> TODAS las promesas terminadas", value)
    }, function(reason) {
      console.log("Ups...hubo algún error!", reason)
    });
```


**fetch**
Hoy día la manera estándar de acceder a datos en el servidor desde nuestro frontend es con fetch(), una nueva API del navegador que funciona gracias a una forma moderna de manejar la asincronía de JavaScript llamada Promesas. 

La API Fetch proporciona una interfaz JavaScript para acceder y manipular partes del canal HTTP, tales como peticiones y respuestas. También provee un método global fetch() que proporciona una forma fácil y lógica de obtener recursos de forma asíncrona por la red.

Puntualizar que la llamada a `fetch()` devuelve un objeto tipo `Promise`, con lo que todo lo visto anteriormente se puede seguir aplicando.

- [MDN | fetch](https://developer.mozilla.org/es/docs/Web/API/Fetch_API/Utilizando_Fetch)
- [fetch](https://javascript.info/fetch)
- [Utilizando_Fetch](https://developer.mozilla.org/es/docs/Web/API/Fetch_API/Utilizando_Fetch)

Fetch devuelve una promesa, pero en el `then()` no trae los resultados parseados, debemos esperar a que termine el método `then()` e indicar el método de decodificación de los datos.

Ejemplo, si trabajas con JSON entonces devuelve `res.json()` 

Petición básica GET con fetch()
```javascript
fetch('https://fakestoreapi.com/products/1')
            .then(res=>res.json())
            .then(json=>console.log(json))
```

Tratando con catch() en caso de error
- [fetch-and-errors](tjvantoll.com/2015/09/13/fetch-and-errors/)
```javascript
fetch("http://httpstat.us/500")
    .then(function(response) {
        if (!response.ok) {
            throw Error(response.statusText);
        }
        return response;
    }).then(function(response) {
        console.log("ok");
    }).catch(function(error) {
        console.log(error);
    });
```

Ejemplo con POST

```javascript
fetch('https://jsonplaceholder.typicode.com/posts', {
  method: 'POST',
  body: JSON.stringify({
    title: 'foo',
    body: 'bar',
    userId: 1,
  }),
  headers: {
    'Content-type': 'application/json; charset=UTF-8',
  },
})
  .then((response) => response.json())
  .then((json) => console.log(json));
```

En los viejos tiempos utilizando XMLHttp request:
- [ajax_xmlhttprequest_send](https://www.w3schools.com/xml/ajax_xmlhttprequest_send.asp)

```javascript

function peticion(url) {
    var xmlHttp = new XMLHttpRequest();

    xmlHttp.onreadystatechange = function() {

        if (xmlHttp.readyState === 4 && xmlHttp.status === 200) {
            console.info(JSON.parse(xmlHttp.responseText));
        } else if (xmlHttp.readyState === 4 && xmlHttp.status === 404) {
            console.error("eRROR!! NO ENCONTRADO! 404");
            console.info(JSON.parse(xmlHttp.responseText));
        }
    };
    xmlHttp.open("GET", url, true);
    xmlHttp.send();
}

peticion("<---TU URL AQUÍ---->");
```

**APIs de prueba:**
- [fakestoreapi](https://fakestoreapi.com/)
- [dog-api](https://dog.ceo/dog-api/)
- [randomuser](https://randomuser.me/documentation)
- [jsonplaceholder](https://jsonplaceholder.typicode.com/guide/)
- [rick and Morty](https://rickandmortyapi.com/api/character)
- [pokeapi](https://pokeapi.co/)
- [public-apis](https://github.com/public-apis/public-apis)


![fetchxhr](../../assets/js_avanzado/clase4/xhrfetchtstarwars.jpeg)


### Ejercicios

#### 1. Quiero un perrito, pero no se qué raza escoger, ¿me ayudas?

En este ejercicio utilizaremos la API de https://dog.ceo/dog-api/. Leyendo su documentación, deberás hacer lo siguiente: 

- Imprimir por consola la lista de razas de todos los perros. 
- Imprimir por consola una imagen random de una raza. 
- Imprimir por consola todas las imágenes de una raza concreta. 

¿Y si ahora te pidieramos que podamos poner otra raza en la url para que nos busque otras imágenes? Adapta las urls que ya tenías para que puedas pasarle argumentos.  

Recuerda que para estos ejercicios deberás utilizar fetch. Al haber conseguido que se imprima por consola, el siguiente paso será que se muestren en pantalla con las herramientas que nos ofrece el arbol DOM. 


#### 2. ¿Quieres saber mi información? Aquí la tienes. 

Para este ejercicio vamos a utilizar la API de usuarios de GitHub, la cual tiene esta URL: https://api.github.com/users/{username}. {username} es el nombre del usuario en GitHub, por lo que si quieres buscar a cualquier usuario, solo tienes que ponerlo en la url. Por ejemplo,  https://api.github.com/users/silvialcastilla. Si ponéis esta URL en una nueva pestaña del navegador podréis observar qué datos nos devuelve el API.

Lo primero que haremos será crear un input de tipo texto y un botón para buscar. El usuario escribirá en el input el nombre de usuario de GitHub que quiera buscar. Después crearemos una función que se ejecute cuando se pulse el botón buscar y que contenga una petición a la API para obtener información de ese usuario y así mostrarla en nuestra página:

Lo que queremos que se imprima por consola será:
- nombre
- número de repositorios
- avatar (imagen)

Si ya has obtenido toda la información, utiliza las herramientas del arbol DOM para que esta información aparezca en la pantalla.

#### 3. Promesas, promesas y más promesas.

Dada una lista de usuarios de github guardada en una array, utiliza 'https://api.github.com/users/${name}' para obtener el nombre de cada usuario.

- Objetivo: Usar Promise.all()
- Recordatorio: Una llamada a fetch() devuelve un objeto promesa.
- Pregunta. ¿cuántas promesas tendremos?

Hasta que no se resuelvan todas las promesas desencadenadas por cada fetch(), no se cargarán los datos.

Pasos: 
- Mapear el array y hacer un fetch() para cada usuario. Esto nos de vuelve un array lleno de promesas.
- Con Promise.all() harás que se tenga que resolver todo el proceso de peticiones a GitHub a la vez.
- Cuando Promise.all() haya terminado: 
  1. Consigue que se imprima por consola la url del repositorio de cada usuario.
  2. Consigue que se imprima por consola el nombre de cada usuario. 