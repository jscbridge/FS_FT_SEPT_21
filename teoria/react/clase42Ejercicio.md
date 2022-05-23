![logotipo de The Bridge](https://user-images.githubusercontent.com/27650532/77754601-e8365180-702b-11ea-8bed-5bc14a43f869.png  "logotipo de The Bridge")
# [Bootcamp Web Developer Full Stack](https://www.thebridge.tech/bootcamps/bootcamp-fullstack-developer/)
### JS, ES6, Node.js, Frontend, Backend, Express, React, MERN, testing, DevOps


## Clase 42

### React: Ejercicio

### EJERCICIO: PokeApp con React Funcional (III)

![img](../../assets/react/clase40/Pokemon.jpg)

- [pokeapi](https://pokeapi.co/)

- Para esta fase, en lugar de pulsar un botón para hacer la búsqueda vamos a dejar que las búsquedas se hagan solas en función de lo que escriba el usuario.
- Eliminamos el botón.
- Cuando escribamos, la petición deberá realizarse según escribimos. 
- Una vez que consigamos que esas peticiones se hagan con cada pulsación. Cuando obtengamos el pokemon deseado, éste deberá concatenarse a la lista como en la fase anterior.
- Como anteriormente, utiliza el componente ListaPokemon, que deberá dibujar una lista con todas las Card de datos e imagen del Pokemon.

Debounce:
- Lógicamente una petición por pulsación es demasiado. Es probable que con ese nivel de peticiones alcancemos el máximo de peticiones permitidos por la Api en poco tiempo. Lo siguiente que haremos será evitar que con cada pulsación se haga una petición. La lógica para hacer esto será que si entre pulsaciones pasa más de un segundo y medio (o el tiempo que queráis) se haga la petición a la Api de lo que haya almacenado en el estado del input en ese momento.
- Investiga qué es y cómo es la lógica de un `Debounce` para implementarla y conseguir el paso anterior. Esta función es la que nos permitirá conseguir que solo tras la última pulsación de más de un tiempo determinado se haga la petición.
- OJO: Cuando consigas implementar la función `debounce` para no colapsar la api a peticiones implementa lo siguiente: si el input está vacío no se hará ninguna petición.
- Cuando escribamos un pokemon en el input que ya exista en nuestra lista de pokemons tampoco tenemos que hacer esa petición.

- NOTA: El ejercicio se debe hacer con React funcional y como mínimo con los Hooks `useState()` y `useEffect()`
- Para practicar, puedes investigar y hacer uso de cualquier otro Hook (tanto propio como de terceros) que tenga sentido para este ejercicio




