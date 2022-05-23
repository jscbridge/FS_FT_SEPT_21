![logotipo de The Bridge](https://user-images.githubusercontent.com/27650532/77754601-e8365180-702b-11ea-8bed-5bc14a43f869.png  "logotipo de The Bridge")


# [Bootcamp Web Developer Full Stack](https://www.thebridge.tech/bootcamps/bootcamp-fullstack-developer/)
### JS, ES6, Node.js, Frontend, Backend, Express, React, MERN, testing, DevOps

## Clase 3

**Destructuración - arrays**

![img](../../assets/js_avanzado/clase3/destructuring.jpeg)
- [MDN | Destructuring_assignment](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Operadores/Destructuring_assignment)

```javascript

let [a, b] = [10, 20];

// Guarda a=3 y b=6
let list = [ 3, 5, 6 ]
let [ a, , b ] = list

// Asignar nombres de parámetros a objetos que pasas por una función
function imprime ([ name, val ]) {
	console.log(`${name}, buenos ${val}`)
}
imprime([ "hola", "dias" ]);

// Fail-Soft Destructuring
let list2 = [ 33, 2 ]
let [ a = 3, b = 4, c = 5, d ] = list2
```

**Destructuración - objetos**
```javascript
// asignación básica
const user = {
id: 42,
is_verified: true
};

const {id, is_verified} = user;

console.log(id); // 42
console.log(is_verified); // true 
```
```javascript
// asignar nuevos nombres de variable
const o = {p: 42, q: true};
const {p: foo, q: bar} = o;

console.log(foo); // 42 
console.log(bar); // true
```
```javascript
// Valores predeterminados
const {a = 10, b = 5} = {a: 3};

console.log(a); // 3
console.log(b); // 5
```

**Spread Operator**
>El operador de propagación spread operator permite que una expresión sea expandida en situaciones donde se esperan múltiples argumentos (llamadas a funciones) o múltiples elementos (arrays literales).- [MDN | Spread_operator](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Operadores/Spread_operator)

- [operador-spread-es6](https://desarrolloweb.com/articulos/operador-spread-es6.html)
- [javascript-spread-operator](https://www.geeksforgeeks.org/javascript-spread-operator/)

```javascript
// Ejemplo 1
[a, b, ...rest] = [10, 20, 30, 40, 50];
console.log(rest);  // [30, 40, 50]

// Ejemplo 2

let miArray = [2, 5, 7, 1, 9];
let minimo = Math.min(...miArray);

//Ejemplo 3 

let misConocimientos = ['variables', 'operadores', 'estructuras de control', 'funciones'];
let aprendido = ['rest operator', 'spread operator'];
let misConocimientosAmpliados = [...misConocimientos, ...aprendido, 'otra cosa más'];

//Ejemplo 4 - mergeando objetos
const user1 = { 
    name: 'Jen', 
    age: 22, 
}; 
  
const user2 = { 
    name: "Andrew", 
    location: "Philadelphia" 
}; 

const mergedUsers = {...user1, ...user2}; 
console.log(mergedUsers) 
```

**Rest operator**
>El operador Rest es exactamente igual a la sintaxis del operador de Spread, y se utiliza para desestructurar arrays y objetos. En cierto modo, Rest es lo contrario de spread. Spread 'expande' un array en sus elementos, y Rest recoge múltiples elementos y los 'condensa' en uno solo.- [MDN | Spread_operator](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Operadores/Spread_operator)
- [spread-vs-rest-parameters-en-es6](https://www.arquitecturajava.com/spread-vs-rest-parameters-en-es6/)
- [javascripts-three-dots-spread-vs-rest-operators](https://scotch.io/bar-talk/javascripts-three-dots-spread-vs-rest-operators543)


```javascript
function opera (x, y, ...a) {
	    return (x + y) * a.length
	}
```

```javascript
function add(...rest) {
  let total = 0;

  for (let i=0;i<rest.length;i++) {
  total += rest[i];
  }
  return total
}

add(1) // returns 1
add(1,2) // returns 3
add(1, 2, 3, 4, 5) // returns 15
```

```javascript
function xyz(x, y, ...z) {
  console.log(x, ' ', y); // hey hello

  console.log(z); // ["wassup", "goodmorning", "hi", "howdy"]
  console.log(z[0]); // wassup
  console.log(z.length); // 4
}

xyz("hey", "hello", "wassup", "goodmorning", "hi", "howdy")
```

**Operador condicional (ternario)**
- [MDN | Conditional_Operator](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Operadores/Conditional_Operator)

```javascript
// Ejemplo 1
let esCliente = true;
console.info("El pago son  " + (esCliente ? "10.00€" : "20.00€"));

// Ejemplo 2
let esCliente = true;
let esAdulto = true;
console.info(esCliente ? "Debes pagar 10.00€" : esAdulto ? "Envíe su solicitd" : "Sorry, espera a hacerte mayor :)");

// Ejemplo 3
let mensaje,
esCliente = true;

esCliente ? (
	mensaje = "debe pagar 10.00€",
	console.info(mensaje)
) : (
	mensaje = "Sebe pagar 20.00€",
	console.info(mensaje)
);
  
```

**Parámetros opcionales**
```javascript
function f (x, y = 3, z = 22) {
	return x + y + z
}
```

**Bucles - for vs for..of vs for..in vs forEach**
  - [for vs for-each vs for-in vs for-of in javascript](https://thecodebarbarian.com/for-vs-for-each-vs-for-in-vs-for-of-in-javascript)
  - [MDN | forEach](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Array/forEach)
  - [MDN | for...of](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Sentencias/for...of)
  - [MDN | for...in](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Sentencias/for...in)


Distintas formas de hacer lo mismo
```javascript
/* 
  for (let i = 0; i < arr.length; ++i)
  arr.forEach((v, i) => { //Codigo aqui })
  for (let i in arr)
  for (const v of arr) 
*/
```
**for..in**
Con for/for..in hay que acceder por posicion del array
```javascript
  const arr = ['a', 'b', 'c'];
  for (let i = 0; i < arr.length; ++i) {
  console.log(arr[i]);
}

for (let i in arr) {
  console.log(arr[i]);
}
```
```javascript
const objeto = { a: 1, b: 2, c: 3 };

for (const clave in objeto) {
  console.log(`${clave}: ${objeto[clave]}`);
```

```javascript
let arr = [4, 5, 9];
arr.foo = "hello";

// Devuelve los índices/claves
for (let i in arr) {
    console.log(i);
    // "0", "1", "2", "foo"
}

```
**for...of**
```javascript

// for..of. Devuelve el contenido en cada posición
//Iteración sobre valores 
let numeros = [99, 22, 33];
for (let num of numeros) {
    console.log(num);
    // "99", "22", "33"
}

const arr = ['a', 'b', 'c'];
arr.test = 'abc';

// Prints "a, b, c"
for (let i = 0; i < arr.length; ++i) {
  console.log(arr[i]);
}

// Prints "a, b, c"
for (const element of arr) {
  console.log(element);
}

let coches = [{name:'Peugeot'}, {name:'BMW'}];
for (let coche of coches) {
console.log(coche.name)
}
```

**Array.prototype.forEach()**
- [MDN | Array.prototype.forEach()](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Array/forEach)
- [javascript-map-vs-foreach](https://codeburst.io/javascript-map-vs-foreach-f38111822c0f)

```javascript
  let numbers = [65, 44, 12, 4];
  numbers.forEach(myFunction)

  function myFunction(item, index, arr) {
    arr[index] = item * 10;
}

// Prints "a, b, c"
const arr = ['a', 'b', 'c'];
arr.forEach((element, i) => console.log(`Letra ${element} en posición ${i}`));
```
![img](../../assets/js_avanzado/clase3/es6meme.jpg)


### Ejercicios

## 1. Ejercicios destructuring

1. Dado el siguiente objeto:
```javascript
const empleados = [
  {"name":"Luis", "email":"Luis@gmail.com"},
  {"name":"Ana", "email":"Ana@gmail.com"},
  {"name":"Andrea", "email":"Andrea@gmail.com"}
]
```
- Extrae la empleada Ana completa
```javascript
{"name":"Ana", "email":"Ana@gmail.com"}
```
- Extrae el email del empleado Luis --> Luis@gmail.com


2. Usa destructuración para intercambiar los valores de a y b
```javascript
// Inicialmente
let a = 5
let b = 3

// Al final
let a = 3
let b = 5
```

3. Dado el siguiente objeto:
```javascript
const HIGH_TEMPERATURES = {
  yesterday: 30,
  today: 35,
  tomorrow: 32
};
```
- Cambiar las siguientes líneas para guardar mediante destructuración los valores de temperaturas en las variables `maximaHoy` y `maximaManana`
``` javascript
const maximaHoy = HIGH_TEMPERATURES.today;
const maximaManana = HIGH_TEMPERATURES.tomorrow; 
console.log(maximaHoy)
console.log(maximaManana)
```

## 2. Ejercicios spread/rest 

1. Escribe una función llamada `sumEveryOther` que pueda recibir cualquier cantidad de números y devuelva la suma de todos los demás argumentos.
```javascript
sumEveryOther(6, 8, 2, 3, 1); //20
sumEveryOther(11, 3, 12); //26
```
2. Escribe una función llamada `addOnlyNums` que pueda recibir cualquier número de argumentos (incluyendo números y strings y retorne la suma solo de los números.
```javascript
addOnlyNums(1, 'perro', 2, 4); //7
```
3. Escribe una función llamada `countTheArgs` que pueda recibir cualquier número de argumentos y devuelva un número que indique cuántos argumentos ha recibido.
```javascript
countTheArgs('gato', 'perro'); //2
countTheArgs('gato', 'perro', 'pollo', 'oso'); //4
```
4. Escribe una función llamada `combineTwoArrays` que reciba dos array cómo argumentos y devuelva solo un array que combine los dos (usando spread operator).

5.  Escriba una función llamada `onlyUniques` que acepte cualquier número de argumentos y devuelva un array de elementos únicos, sin repetidos.
```javascript
onlyUniques('gato', 'pollo', 'cerdo', 'cerdo'); //['gato', 'pollo', 'cerdo']
onlyUniques(1, 1, 2, 2, 3, 6, 7, 8); //[1, 2, 3, 6, 7, 8]
```
6.  Escriba una función llamada `combineAllArrays` que pueda recibir cualquier cantidad de arrays como argumentos y los combine todos en un solo array.
```javascript
combineAllArrays([3, 6, 7, 8],[2, 7, 3, 1]) // [3, 6, 7, 8, 2, 7, 3, 1]
combineAllArrays([2, 7, 3, 1],[2, 7, 4, 12],[2, 44, 22, 7, 3, 1]); // [2, 7, 3, 1, 2, 7, 4, 12, 2, 44, 22, 7, 3, 1]
```
7. Escriba una función llamada `sumAndSquare` que reciba cualquier número de argumentos, los eleve al cuadrado y devuelva la suma de todos los valores cuadrados.


**Más ejercicios extra ES6**
- [Katas ES6](https://jskatas.org/#bundle-es6-katas)


