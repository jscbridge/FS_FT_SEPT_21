![logotipo de The Bridge](https://user-images.githubusercontent.com/27650532/77754601-e8365180-702b-11ea-8bed-5bc14a43f869.png  "logotipo de The Bridge")


# [Bootcamp Web Developer Full Stack](https://www.thebridge.tech/bootcamps/bootcamp-fullstack-developer/)
### JS, ES6, Node.js, Frontend, Backend, Express, React, MERN, testing, DevOps

## Clase 6

### ECMA6: async/await

![Leaflet](../../assets/js_avanzado/clase6/asyncawait_lion_king2.jpg)

- [MDN | funcion_asincrona](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Sentencias/funcion_asincrona)
- [MDN | Async_await](https://developer.mozilla.org/es/docs/Learn/JavaScript/Asynchronous/Async_await)
- [async-functions](https://developers.google.com/web/fundamentals/primers/async-functions?hl=es)
- [javascript-fetch-api-and-using-asyncawait](https://dmitripavlutin.com/javascript-fetch-async-await/)
- [JavaScript Info | async-await](https://javascript.info/async-await)

- Fetch tradicional
```javascript
function getUser(name){
 fetch(`https://api.github.com/users/${name}`)
  .then(function(response) {
    return response.json();
  })
  .then(function(json) {
    console.log(json);
  });
};
getUser('yourUsernameHere')
```
- Usando async/await.
Si usas la palabra clave `async` antes de una definición de función, luego puedes usar `await` dentro de la función. Cuando `await` (esperas) una promesa, la función se pausa de una forma que no bloquea hasta que la promesa se detenga. Si la promesa se completa, recibes de vuelta el valor. Si la promesa rechaza, se arroja el valor rechazado.

```javascript
async function getUserAsync(name) 
{
  let response = await fetch(`https://api.github.com/users/${name}`);
  let data = await response.json()
  return data;
}

getUserAsync('yourUsernameHere')
  .then(data => console.log(data))
  .catch(error => console.log("hubo un error"+error));
```

- Con try/catch
```javascript
async function getUserAsync2(name) {
    try {
        let response = await fetch(`https://api.github.com/users/${name}`);
        let data = await response.json()
        return data;    
    }
    catch (error) {
        console.log(`ERROR: ${error.stack}`);
    }
}
getUserAsync2('yourUsernameHere')
.then(data=>console.log(data))
```

![Leaflet](../../assets/js_avanzado/clase6/asyncawait_lion_king.jpg)


### ECMA6: Objetos Map y Set
Desde la llegada de la especificación ECMAScript 6 disponemos de nuevos tipos de estructura, como Set y Map

Recursos:
- [objetos-map-set](https://www.todojs.com/objetos-map-set/)
 -[understanding-map-and-set-objects-in-javascript-es](https://www.digitalocean.com/community/tutorials/understanding-map-and-set-objects-in-javascript-es)

### Objeto Set
En un array podemos almacenar valores duplicados, mientras que en Set no está permitido.

A diferencia de los arrays en un objeto Set no podemos acceder directamente a un elemento. Un Set son una colección de claves. Por ello en un objeto Set sólo podemos iterar a través de todos sus elementos por medio de un loop.

S quieres disponer de un objeto, que puedas hacer lecturas, borrados, o modificaciones muy concretas deberás utilizar un array. En caso de que sólo desees hacer principalmente lecturas usa un Set.

- [MDN | Set](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Set)
- [Array vs Set](https://victordeandres.es/post/array-vs-set)
```javascript
	let mySet = new Set()
	mySet.add("patatas")
    .add("pescado")
    .add("naranjas")
	
	console.log(mySet.has("patatas")) // true

    // Iterar con for of
	for (let key of mySet.values()) // insertion order
	    console.log(key)
    //Iterar con forEach
    mySet.forEach( myValue => console.log(myValue) );
    

```
```javascript
const mySet = new Set(); // Se inicializa un set vacío.

    const mySet = new Set([1, 2, 2, 3])       
    // Se inicializa un set nuevo set con los valores 1,2,3.
    // Recuerda que un set no permite valores duplicados.

    const  mySet = new Set(1)                   
    // Error. Siempre debemos utilizar un objeto iterable en el constructor. 
```

### Objeto Map
Datos independientes con una estructura clave/valor. Cualquier valor(tanto objetos como valores primitivos) pueden ser usados como clave o valor.

- [MDN | Map](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Map)

```javascript
	let miMap = new Map();
	let miArray = ["patata","pescado"];

	miMap.set('nombre', 'Alex');
    miMap.set('apellidos', 'Reyes');
	miMap.set(miArray, [500, "hola", true, false]);

	console.log(miMap.get(miArray)); // [500, "hola", true, false]
	console.log(miMap.get('cadena')); // Hola!

	console.log(miMap.size); // 2

    // Iterar
    miMap.forEach(function(valor, clave) {
    console.log(clave + ' = ' + valor);
    });

	miMap.delete('cadena'); // Borrar
	console.log(miMap.size); // 2
```
Objetos como clave
```javascript
	
var obj1 = {
    a: 1,
    b: 2
};
 
var obj2 = {
    a: 1,
    b: 2
};
 
var map = new Map();
map.set( obj1, 1 );
 
console.log( 'map.has(obj1) = ', map.has(obj1) );    // true
console.log( 'map.has(obj2) = ', map.has(obj2) );    // false
```

### Set vs Map vs Array
```javascript
	var array = [1, 22, 34, 34];
    console.log(array.length)//4
	
	var mySet = new Set(array); //  [1, 22, 34]
	console.log(mySet.size)// 3
	
	var myMap = new Map();
	myMap.set('a', 1);
	myMap.set('b', 2);
	myMap.set('c', 3);
	myMap.set('C', 3);
	myMap.set('a', 4); // a, 4; b, 2; c: 3, C: 3
	console.log(myMap.size)// 4
```

### Ejercicios

#### async/await con Pokémon
![batalla](../../assets/js_avanzado/clase6/Pokemon.jpg)
Utilizando la api de Pokemons `https://pokeapi.co/` y usando sólo `async/await`:
- Obtener un Pokemon de manera aleatoria (fetch)
- Tras obtener dicho Pokémon
    - Obten su imágen correspondiente 
    - Obtener nombre del Pokémon
- Dibujar nombre e imágen del Pokémon en el DOM
- OJO!! Te tocará estudiar cómo funciona la API de Pokémon para encontrar la imágen. Puede que tengas que hacer más de un fetch!! (depende de la ruta de consulta que uses)
```javascript
...
"sprites": {
    "back_female": "http://pokeapi.co/media/sprites/pokemon/back/female/25.png",
    "back_shiny_female": "http://pokeapi.co/media/sprites/pokemon/back/shiny/female/25.png",
    "back_default": "http://pokeapi.co/media/sprites/pokemon/back/25.png",
    "front_female": "http://pokeapi.co/media/sprites/pokemon/female/25.png",
    "front_shiny_female": "http://pokeapi.co/media/sprites/pokemon/shiny/female/25.png",
    "back_shiny": "http://pokeapi.co/media/sprites/pokemon/back/shiny/25.png",
    "front_default": "http://pokeapi.co/media/sprites/pokemon/25.png",
    "front_shiny": "http://pokeapi.co/media/sprites/pokemon/shiny/25.png"
  },
...
```

### async/await - batalla Pokémon vs perritos
![batalla](../../assets/js_avanzado/clase6/batalla.jpeg)

Usando la API de Pokémon queremos hacer una batalla particular entre perritos y Pokémons. Recordemos que la API de perritos era 'https://dog.ceo/dog-api/'.

Tareas:
- Obtener de manera random la imágen de un perrito (fetch)
- Obtener de manera random la imágen de un Pokémon (otro fetch)
- Dibujar en el DOM la batalla. "Pikachu" vs "Pug". ¿Te imaginas?
