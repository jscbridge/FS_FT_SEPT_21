![logotipo de The Bridge](https://user-images.githubusercontent.com/27650532/77754601-e8365180-702b-11ea-8bed-5bc14a43f869.png  "logotipo de The Bridge")


# [Bootcamp Web Developer Full Stack](https://www.thebridge.tech/bootcamps/bootcamp-fullstack-developer/)
### JS, ES6, Node.js, Frontend, Backend, Express, React, MERN, testing, DevOps

## Clase 2

### Programación funcional
![img](../../assets/js_avanzado/clase2/functional_programming.png)

> La Programación Funcional se refiere a la evaluación declarativa de funciones puras para crear programas inmutables y así evitar efectos secundarios que son observados externamente.- [El Abismo de Null](https://elabismodenull.wordpress.com/2016/10/12/la-programacion-funcional-en-javascript/)

## Funciones puras

En programación, las Funciones Puras son aquellas que cumplen con dos requisitos básicos:
- Dado unos parámetros de entrada de idéntico valor, la función siempre devolverá el mismo resultado.
- El cómputo de la función, su lógica, no implica ningún efecto observable colateral fuera de ella.

Las funciones puras son muy previsibles y testeables

Ejemplo:
```javascript
function pureFoo ( a, b ) {
    return a + b;
}
 
console.info( pureFoo( 2, 4 ) ); // 6
console.info( pureFoo( 3, 6 ) ); // 9
console.info( pureFoo( 2, 4 ) ); // 6
```

Recursos:
- [las-funciones-puras-en-javascript-concepto-ejemplos-y-beneficios](http://www.etnassoft.com/2016/06/21/las-funciones-puras-en-javascript-concepto-ejemplos-y-beneficios/)
- [javascript-pure-functions](https://willtaylor.blog/javascript-pure-functions/)


Ventajas:
- Código más conciso y expresivo
- Que el estado sea inmutable, evita muchos errores (sin efectos colaterales)
- Entrada y salida; Las funciones reciben parámetros y devuelven un resultado.
- Las funciones puras son muy previsibles y testeables
- Código infinitamente más expresivo
- Proceso de depuración simplificado
- Fomenta mucho la descomposición de las tareas complejas
- Hacemos uso de composiciones partiendo de fragmentos pequeños y especializados

Desventajas:
- Falta soporte nativo
- Paradigma menos extendido (de momento...)
- Propensión a los errores, ya que JS no es estrcito con el pardaigma funcional
- Tipado debil. Puede ser preocupante
- Cercano a las matemáticas
- Gestión de recursos
- Necesidad de realizar abstracciones

Más ejemplos:

```javascript
// Función pura
console.info( Math.min( 0, 150, 30, 20, -8, -200 ) ); // -200
console.info( Math.max( 0, 150, 30, 20, -8, -200 ) ); // 150
console.info( Math.sqrt( 16 ) ); // 4
// Función no pura
console.info( Math.random() ); // 0.014685770236463336
console.info( Math.random() ); // 0.7129402960991972
```

```javascript
//Función pura
const incremento = n => n + 1;
incremento(1); // 2

// Función no pura
let numero = 1;
const incremento = () => numero += 1;
incremento(); // 2
```
```javascript
//Función pura
let saludos = (nombre) => `Hola, ${nombre}!`
saludos('Alex') // 'Hola, Alex!'

// Función no pura
window.nombre = 'Alex'
let saludos = () => `Hola, ${window.nombre}!`
saludos() // 'Hola, Alex!'
```

## Arrow functions - ECMA6
Características:
- No pueden ser usadas como constructores
- No tienen una propiedad de prototipo `prototype`
- No pueden tener saltos de línea
- Retorno de objetos literales
- Orden de parseo
- Siempre son anónimas
- return implicito en declaración inline

Recursos:
- [MDN | Arrow_functions](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Funciones/Arrow_functions)
- [arrow-functions-es6](https://desarrolloweb.com/articulos/arrow-functions-es6.html)

## Arrow functions - Sintaxis básica
```javascript
(param1, param2, paramN) => {declaraciones} 
(param1, param2, paramN) => expresion
// Equivalente a: () => { return expresion; } 

// Parénteis opcional si sólo dispone de un argumento: singleParam => { statements } 
singleParam => expresion 

// Una función sin argumentos requiere paréntesis: 
() => { declaraciones }
```
```javascript
const func = x => x * x;                  
// sintaxis de cuerpo conciso, el "return" está implícito

const func = (x, y) => { return x + y; }; 
// con cuerpo de bloque, se necesita "return" explícito
```

```javascript
let numeros = [2,5,6,7,8]
impares  = numeros.map(v => v + 1);
pares = numeros.map(v => ({ even: v, odd: v + 1 }))
otrosNumeros  = numeros.map((v, i) => v + i)
```


```javascript
let numeros = [3,6,,5,10,77]
let multiplos = []
numeros.forEach((v) => {
    if (v % 5 === 0)
        this.multiplos.push(v)
})
```

```javascript
	const odds = [1,2,3,4,5].filter(num => num % 2);
	console.log(odds); // Array [ 1, 3, 5 ]
```

```javascript
// No hay constructores
const Foo = () => {};
const foo = new Foo(); // TypeError: Foo is not a constructor
```
```javascript
// No hay prototipos 
const Foo = () => {};
console.log(Foo.prototype); // undefined
```

```javascript
// No puede haber salto de línea
const func = ()
       => 1; 
// SyntaxError: expected expression, got '=>'
```

```javascript
// Objetos devueltos
const func = () => {  foo: 1  };               
// Al llamar func() retorna undefined!

// Funciona correctamente
const func = () => ({ foo: 1 });
```
```javascript
// Orden de parseo
let callback;

callback = callback || function() {}; // ok

callback = callback || () => {};      
// SyntaxError: invalid arrow-function arguments

callback = callback || (() => {});    // ok
```

## Array methods: map, filter, reduce

- [learn-map-filter-and-reduce-in-javascript](https://medium.com/@joomiguelcunha/learn-map-filter-and-reduce-in-javascript-ea59009593c4)
- [functional-programming-in-js-map-filter-reduce](https://hackernoon.com/functional-programming-in-js-map-filter-reduce-pt-5-308a205fdd5f)



## Array methods: map
- [ MDN | Array.proptotype.map()](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Array/map)


Mapea uno a uno los elementos de un array y los transforma (mapea) según necesitemos
```javascript
let productos = ["patatas", "pescado", "naranjas", "manzana"];
let resultado = productos.map(function (producto){return producto + " modificado!"});
console.log(resultado);
```
```javascript


// Usando MAP
let arr = [1, 2, 3, 4, 5, 6, 7];
let multiplyBy2 = n => n * 2;

let arrTimes2 = arr.map(multiplyBy2);
console.log(arrTimes2); // [2, 4, 6, 8, 10, 12, 14]


// Antes de MAP
let arr = [1, 2, 3, 4, 5, 6, 7];
let arrTimes2 = [];
let multiplyBy2 = n => n * 2;

for (let i = 0; i < arr.length; i++) {
    let result = multiplyBy2(arr[i]);
    arrTimes2.push(result);
}
console.log(arrTimes2); // [2, 4, 6, 8, 10, 12, 14]

```

## Array methods: filter
- [MDN | Array.proptotype.filter()](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Array/filter)

Crea un nuevo array (filtra) con aquellos elementos que cumplan la condición
```javascript
function validar(elemento) {
  return elemento >= 10;
}
let filtrados = [false, 22, 4, 2, null, "Bye"].filter(validar);
```

```javascript
//Con FILTER
let words = ['Hola', 'bienvenidos', 'queridos', 'FullStack', 'Developers'];

let longWords = words.filter(word => {
    return word.length > 6;
});

console.log(longWords); //["bienvenidos", "queridos", "FullStack", "Developers"]

// Antes de FILTER
let words = ['Hola', 'bienvenidos', 'queridos', 'FullStack', 'Developers'];
let longWords = [];

for (let i = 0; i < words.length; i++) {
    if (words[i].length > 6) {
        longWords.push(words[i]);
    }
}
console.log(longWords); // ["bienvenidos", "queridos", "FullStack", "Developers"]
```

## Array methods: reduce
- [MDN | Array.prototype.reduce()](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Array/reduce)


Aplica una función a un acumulador y a cada valor de un array para reducirlo a un único valor. En este ejemplo, se hace la suma de todos los elementos del array


```javascript
// Antes de REDUCE
let lista = [2,-1,1,3,5,8];
let acumulacion = 0;

for (let i = 0; i < lista.length; i++) {
    acumulacion += lista[i];
}
console.log(acumulacion); // 10

// Usando REDUCE
let lista = [2,-1,1,3,5,8];
let acumulado = lista.reduce(function(anterior, actual, indice, vector){
  return anterior + actual;
});
console.log(acumulado); // 18
```


## Ejemplos reales - Map, Filter, Reduce
- [sneak-peak-of-map-filter-and-reduce](https://levelup.gitconnected.com/sneak-peak-of-map-filter-and-reduce-in-javascript-79d38181a48)

## Debugging
- [Comenzar a depurar JavaScript en Chrome DevTools](https://developers.google.com/web/tools/chrome-devtools/javascript?hl=es)
- [Cómo recorrer tu código](https://developers.google.com/web/tools/chrome-devtools/javascript/step-code?hl=es-419)


### Ejercicios MAP, FILTER, REDUCE

## 1. Ejercicios Map

- Dado el siguiente array, crear otro que sea el resultado de elevar cada número a si mismo

```javascript
const numbers = [ 4, 5, 6, 7, 8, 9, 10];
// [256, 3125, 46656, 823543, 16777216, 387420489, 10000000000]
```

- Dado el siguiente array, generar un segundo array que consiga generar de salida el resultado esperado

```js
const foodList = ['Pizza', 'Ramen', 'Paella', 'Entrecot'];

//Resultado esperado
/* [
    'Como soy de Italia, amo comer Pizza',
    'Como soy de Japón, amo comer Ramen',
    'Como soy de Valencia, amo comer Paella',
    'Aunque no como carne, el Entrecot es sabroso'
   ]
*/
```

- Dado el siguiente array, crear un segundo array que forme frases como en el ejemplo accediendo a las propiedades del objeto proporcionado:

```javascript
const staff = [
  {
    name: 'Pepe',
    role: 'The Boss',
    hobbies: ['leer', 'ver pelis']
  },
  {
    name: 'Ana',
    role: 'becaria',
    hobbies: ['nadar', 'bailar']
  },
  {
    name: 'Luis',
    role: 'programador',
    hobbies: ['dormir', 'comprar']
  },
  {
    name: 'Carlos',
    role: 'secretario',
    hobbies: ['futbol', 'queso']
  }
];

// Resultado esperado
/*
  [
    'Pepe es TheBoss y le gusta leer y ver pelis',
    'Ana es becaria y le gusta nadar y bailar',
    'Luis es programador y le gusta dormir y comprar',
    'Ana es becaria y le gusta nadar y bailar',
    'Carlos es secretario y le gusta futbol y queso'
  ]
*/
```

## 2. Ejercicios Filter

- Crea un segundo array con que devuelva los impares

```javascript
const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
```

- Dado el siguiente array, genera un segundo array que filtre los platos veganos y saque una sentencia como la del ejemplo

```javascript

const foodList = [
  {
    name: 'Tempeh',
    isVeggie: true
  },
  {
    name: 'Cheesbacon burguer',
    isVeggie: false
  },
  {
    name: 'Tofu burguer',
    isVeggie: true
  },
  {
    name: 'Entrecot',
    isVeggie: false
  }
];


/* [
    'Que rico Tempeh me voy a comer!',
    'Que rica Tofu burguer me voy a comer!'
   ]
*/
```

- Dado el siguiente array, devolver un array con los nombres de los elementos que valgan más de 300 euros

```js

const inventory = [
  {
    name: 'Mobile phone',
    price: 199
  },
  {
    name: 'TV Samsung,
    price: 459
  },
  {
    name: 'Viaje a cancún',
    price: 600
  },
  {
    name: 'Mascarilla',
    price: 1
  }
];

/*
  [
    'TV Samsung,',
    'Viaje a Cancún'
  ]
*/
```

## 3. Ejercicios reduce

- Dado el siguiente array, obten la multiplicación de todos los elementos del array

```javascript
const numeros = [39, 2, 4, 25, 62];

// Salida--> 483600
```

- Concatena todos los elementos del array con reduce para que devuelva una sola frase

```js
const sentenceElements = [
  'Me',
  'llamo',
  /* Tu nombre aqui! */,
  'y',
  'quiero',
  'sentir',
  'la',
  'fuerza',
  'con',
  'javascript'
];

// Resultado--> 'Me llamo XX y quiero sentir la fuerza con javascript'
```

- Obtener el monto total de los elementos que pertenecen a catergory "code"

```javascript
const books = [
  {
    name: ' JS for dummies',
    author: 'Emily A. Vander Veer',
    price: 20,
    category: 'code'
  },
  {
    name: 'Don Quijote de la Mancha',
    author: 'Cervantes',
    price: 14,
    category: 'novel'
  },
  {
    name: 'Juego de tronos',
    author: 'George R. Martin',
    price: 32,
    category: 'Fantasy'
  },
  {
    name: 'javascript the good parts',
    author: 'Douglas Crockford',
    price: 40,
    category: 'code'
  }
];
// Resultado --> 60
```
  




