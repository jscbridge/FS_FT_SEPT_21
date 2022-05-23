![logotipo de The Bridge](https://user-images.githubusercontent.com/27650532/77754601-e8365180-702b-11ea-8bed-5bc14a43f869.png  "logotipo de The Bridge")
# [Bootcamp Web Developer Full Stack](https://www.thebridge.tech/bootcamps/bootcamp-fullstack-developer/)
### JS, ES6, Node.js, Frontend, Backend, Express, React, MERN, testing, DevOps



## Clase 37

### React: Routing, lifecycle

![img](../../assets/react/clase34/react.png)


### Routing
- [react router dom](https://reactrouter.com/web/guides/quick-start)
- [react-router-in-5-minutes/](https://www.freecodecamp.org/news/react-router-in-5-minutes/)
- [react-router-complete-guide](https://www.sitepoint.com/react-router-complete-guide/)


### Lifecycle
![img](../../assets/react/clase37/lifecycle.png)
![img](../../assets/react/clase37/react_lifecycle.png)

- [react-axios-react-es](https://www.digitalocean.com/community/tutorials/react-axios-react-es)
https://ricardogeek.com/usando-axios-con-reactjs/
- [react_lifecycle](https://www.w3schools.com/react/react_lifecycle.asp)

- [mount/unmount| codepen](https://embed.plnkr.co/xAJMb1pvEgcO7dUGrX9h/) 
- [componentWillUnmount| codepen](https://codepen.io/Nyxx/pen/JWPvpY)
- [toggle component width componentDidMount & componentWillUnmount| codepen](https://codepen.io/yakim-shu/pen/aborLxW)



#### Montaje (Mounting)

Estos métodos se llaman cuando se crea una instancia de un componente y se inserta en el DOM:

-   constructor()
-   static getDerivedStateFromProps()
-   render()
-   componentDidMount()

Legacy (deprecados)
-   UNSAFE_componentWillMount()

#### Actualización (Updating)

Una actualización puede ser causada por cambios en los props o el estado. Estos métodos se llaman en el siguiente orden cuando un componente se vuelve a renderizar:


-   static getDerivedStateFromProps()
-   shouldComponentUpdate()
-   render()
-   getSnapshotBeforeUpdate()
-   componentDidUpdate()


Legacy (deprecados)

-   UNSAFE_componentWillUpdate()
-   UNSAFE_componentWillReceiveProps()

#### Desmontaje (Unmounting)

Este método es llamado cuando un componente se elimina del DOM:

-   componentWillUnmount()


#### Manejo de errores 

Estos métodos se invocan cuando hay un error durante la renderización, en un método en el ciclo de vida o en el constructor de cualquier componente hijo.


-   static getDerivedStateFromError()
-   componentDidCatch()


Veamos unos ejemplos de uso de cada ciclo de vida en cada ciclo:

#### Ejemplos Montaje (Mounting)

Constructor

```js
import React, { Component } from 'react';

class ClassComponent extends Component {
    constructor(props) {
        super(props);
        this.state = { name: "Fran" }
        // Event binding (Bindear eventos)
        console.log('CONSTRUCTOR')
    }
    
    render() {
        return (
            <h1>Hi {this.state.name}!!</h1>
        );
    }
}

export default ClassComponent;
```

#### Render

```js
import React from 'react';

const Header ({ title }) => <h1>{title}</h1>

export default Header;
```

```js
import React, { Component } from 'react';
import Header from './components/Header';

class ClassComponent extends Component {
    constructor(props) {
        super(props);
        // Event binding (Bindear eventos)
        console.log('CONSTRUCTOR')
    }
    
    render() {
        console.log('RENDER')
        return (
            <>
                <Header title="Titulo"></Header>
                <h1>Hi {this.state.name}!!</h1>
            </>
        );
    }
}

export default ClassComponent;
```

En el método render tambien podemos tener lógica para devolver un contenido u otro:

```js
import React, { Component } from 'react';
import Header from './components/Header';

class ClassComponent extends Component {
    constructor(props) {
        super(props);
        // Event binding (Bindear eventos)
        console.log('CONSTRUCTOR')
    }
    
    render() {
        console.log('RENDER')
        if(false){
            return (
                <>
                    <Header title="Titulo"></Header>
                    <h1>Hi {this.state.name}!!</h1>
                </>
            );
        }
        //Que el render devuelva null solo está disponible desde la versión 16
        else return null
    }
}

export default ClassComponent;
```

Es importante puntualizar que en el método render no debemos nunca actualizar el estado porque obtendríamos un bucle infinito y la consola nos mostrará un error.

#### componentDidMount()

Es muy común realizar en este método las siguientes operadiones:
 
-   Peticiones HTTP
-   Asignación de eventos
-   Actualizacion de estado


```js
import React, { Fragment } from 'react';

const PokemonsApi = ({ lista }) => {
    return (
        <div>
            {
                lista.map(pokemon => 
                        <Fragment key={pokemon.name} >
                            <a href={pokemon.url} alt={pokemon.name + 'image'}> {pokemon.name} </a>
                            <p>{pokemon.url}</p>
                        </Fragment>
                )
            }
        </div>
    );
}

PokemonsApi.defaultProps = {
    lista: []
  }

export default PokemonsApi;
```


```js

import React, { Component } from 'react';
import PokemonsApi from './components/PokemonsApi';

class ClassComponent extends Component {
    constructor(props) {
        super(props);
        this.state = { pokeLista: [] }
        // Event binding (Bindear eventos)
        console.log('CONSTRUCTOR')
    }
    
    async componentDidMount(){
            //Petición HTTP
            // fetch('https://pokeapi.co/api/v2/pokemon')
            //     .then(resp => resp.json())
            //     .then(data => data)
            const resp = await fetch('https://pokeapi.co/api/v2/pokemon');
            const data = await resp.json();
            this.setState({
                pokeLista: data.results
            })
            console.log('componentDidMount');
        }

    render() {
        console.log('RENDER')
        return (
            <PokemonsApi lista={this.state.pokeLista}></PokemonsApi>
        );
    }
}

export default ClassComponent;
```

#### Ejemplo Actualización (Updating)

#### componentDidUpdate 

Este se ejecuta cuando cambia el estado o las props, aunque las props son inmutables desde el componente, estas podrian cambiar desde el padre.

Veamos un ejemplo donde se ejecuta el 'componentDidUpdate' cuando cambia el estado:


```js
import React from 'react';
import './App.css';
import LifeCycleComponent from './components/LifeCycle';

function App() {
      console.log('RENDER')
      const lista = [{ name: 'pokeapi', ulr: 'https://pokeapi.co/' }]
      return (
          <LifeCycleComponent defaultList={lista}></LifeCycleComponent>
      );
    
}

export default App;

```

```js
import React, { Component, Fragment } from 'react';

class LifeCycleComponent extends Component {
    constructor(props) {
        super(props);
        this.state = { pokeLista: this.props.defaultList }
        // Event binding (Bindear eventos)
        console.log('CONSTRUCTOR')
    }
    
    async componentDidMount(){
        const resp = await fetch('https://pokeapi.co/api/v2/pokemon');
        const data = await resp.json();
        this.setState({
            pokeLista: data.results
        })
        console.log('componentDidMount');
    }

    componentDidUpdate(prevProps, prevState){
        console.log('prevProps: ', prevProps, 'prevState: ', prevState)
        console.log('componentDidUpdate');
    }

    handlerLoadPokemons = async () => {
        const resp = await fetch('https://pokeapi.co/api/v2/pokemon');
        const data = await resp.json();
        this.setState({
            pokeLista: data.results
        })
    }

    handlerResetPokemons = () => {
        this.setState({
            pokeLista: []
        })
    }

    render() {
        console.log('RENDER')
        return (
            <div>
                <h1>Lista Pokemon</h1>
                {
                    this.state.pokeLista.map(pokemon => 
                            <Fragment key={pokemon.name} >
                                <a href={pokemon.url} alt={pokemon.name + 'image'}> {pokemon.name} </a>
                                <p>{pokemon.url}</p>
                            </Fragment>
                    )
                }
                <button onClick={this.handlerLoadPokemons}>Load Pokemons</button>
                <button onClick={this.handlerResetPokemons}>Reset Pokemons</button>
            </div>        
        );
    }
}

LifeCycleComponent.defaultProps = {
    defaultList: []
}

export default LifeCycleComponent;
```

Ahora veamos un ejemplo donde se ejecuta el 'componentDidUpdate' cuando cambian los props:


```js
import React, { Component } from 'react';
import LifeCycleComponent from './components/LifeCycle';

class App extends Component {
  
  state = {
    lista: []
  }

  handleClick = () => {
    this.setState({
      lista: [
        {name: "Pokemon1", url: "url"},
        {name: "Pokemon2", url: "url"},
        {name: "Pokemon3", url: "url"},
        {name: "Pokemon4", url: "url"},
        {name: "Pokemon5", url: "url"}
      ]
    })
  }

  render(){
    // const lista = [{ name: 'pokeapi', ulr: 'https://pokeapi.co/' }]
      return (
          <>
            <button onClick={this.handleClick}>Change Props from father</button>
            <LifeCycleComponent defaultList={this.state.lista}></LifeCycleComponent>
          </>
      );
  }
    
}

export default App;
```

```js
import React, { Component, Fragment } from 'react';

class LifeCycleComponent extends Component {
    constructor(props) {
        super(props);
        this.state = { pokeLista: this.props.defaultList }
        // Event binding (Bindear eventos)
        console.log('CONSTRUCTOR')
    }
    
    async componentDidMount(){
        const resp = await fetch('https://pokeapi.co/api/v2/pokemon');
        const data = await resp.json();
        this.setState({
            pokeLista: data.results
        })
        console.log('componentDidMount');
    }

    componentDidUpdate(prevProps, prevState){
        console.log('prevProps: ', prevProps, 'prevState: ', prevState)
        console.log('componentDidUpdate');
    }

    handlerLoadPokemons = async () => {
        const resp = await fetch('https://pokeapi.co/api/v2/pokemon');
        const data = await resp.json();
        this.setState({
            pokeLista: data.results
        })
    }

    handlerResetPokemons = () => {
        this.setState({
            pokeLista: []
        })
    }

    render() {
        console.log('RENDER')
        return (
            <div>
                <h1>Lista Pokemon</h1>
                {
                    this.state.pokeLista.map(pokemon => 
                            <Fragment key={pokemon.name} >
                                <a href={pokemon.url} alt={pokemon.name + 'image'}> {pokemon.name} </a>
                                <p>{pokemon.url}</p>
                            </Fragment>
                    )
                }
                <button onClick={this.handlerLoadPokemons}>Load Pokemons</button>
                <button onClick={this.handlerResetPokemons}>Reset Pokemons</button>
            </div>        
        );
    }
}

LifeCycleComponent.defaultProps = {
    defaultList: []
}

export default LifeCycleComponent;
```

El método 'componentDidUpdate' también se ejecuta cuando se usa un 'forceUpdate()' aunque este rara vez es necesario usarlo si el código esta bien hecho siguiendo buenas practicas asique si nos vemos en la necesidad de usarlo deberiamos replantearnos antes si hay algo que no estemos haciendo bien ya que en la documentación de react se recomienda no usarlo . Veamos un ejemplo:

```js
import React, { Component, Fragment } from 'react';

class LifeCycleComponent extends Component {
    constructor(props) {
        super(props);
        this.state = { pokeLista: this.props.defaultList }
        // Event binding (Bindear eventos)
        console.log('CONSTRUCTOR')
    }
    
    async componentDidMount(){
        //Petición HTTP
        // fetch('https://pokeapi.co/api/v2/pokemon')
        //     .then(resp => resp.json())
        //     .then(data => data)
        const resp = await fetch('https://pokeapi.co/api/v2/pokemon');
        const data = await resp.json();
        this.setState({
            pokeLista: data.results
        })
        console.log('componentDidMount');
    }

    componentDidUpdate(prevProps, prevState){
        console.log('prevProps: ', prevProps, 'prevState: ', prevState)
        console.log('componentDidUpdate');
    }

    handlerLoadPokemons = async () => {
        const resp = await fetch('https://pokeapi.co/api/v2/pokemon');
        const data = await resp.json();
        this.setState({
            pokeLista: data.results
        })
    }

    handlerResetPokemons = () => {
        this.setState({
            pokeLista: []
        })
    }

    handlerUpdate = () => {
        this.forceUpdate()
    }

    render() {
        console.log('RENDER')
        return (
            <div>
                <h1>Lista Pokemon</h1>
                {
                    this.state.pokeLista.map(pokemon => 
                            <Fragment key={pokemon.name} >
                                <a href={pokemon.url} alt={pokemon.name + 'image'}> {pokemon.name} </a>
                                <p>{pokemon.url}</p>
                            </Fragment>
                    )
                }
                <button onClick={this.handlerLoadPokemons}>Load Pokemons</button>
                <button onClick={this.handlerResetPokemons}>Reset Pokemons</button>
                <button onClick={this.handlerUpdate}>Force Update</button>
            </div>        
        );
    }
}

LifeCycleComponent.defaultProps = {
    defaultList: []
}

export default LifeCycleComponent;
```

#### Desmontaje (Unmounting)

componentWillUnmount()

Este método se ejecuta cuando el componente será desmontado. Veamos un ejemplo:

```js
import React, { Component } from 'react';
import LifeCycleComponent from './components/LifeCycle';

class App extends Component {
  
  state = {
    mostrar: false,
    lista: []
  }

  handleShow = () => {
    this.setState({
      mostrar: !this.state.mostrar
    })
  }

  handleClick = () => {
    this.setState({
      lista: [
        {name: "Pokemon1", url: "url"},
        {name: "Pokemon2", url: "url"},
        {name: "Pokemon3", url: "url"},
        {name: "Pokemon4", url: "url"},
        {name: "Pokemon5", url: "url"}
      ]
    })
  }

  render(){
    // const lista = [{ name: 'pokeapi', ulr: 'https://pokeapi.co/' }]
      return (
          <>
            <button onClick={this.handleClick}>Change Props from father</button>
            <button onClick={this.handleShow}>{this.state.show ? 'Ocultar' : 'Mostrar'}</button>
            { this.state.mostrar ? <LifeCycleComponent defaultList={this.state.lista}></LifeCycleComponent> : null }
          </>
      );
  }
    
}

export default App;

```

```js
import React, { Component, Fragment } from 'react';

class LifeCycleComponent extends Component {
    constructor(props) {
        super(props);
        this.state = { pokeLista: this.props.defaultList }
        // Event binding (Bindear eventos)
        console.log('CONSTRUCTOR')
    }
    
    async componentDidMount(){
        //Petición HTTP
        // fetch('https://pokeapi.co/api/v2/pokemon')
        //     .then(resp => resp.json())
        //     .then(data => data)
        const resp = await fetch('https://pokeapi.co/api/v2/pokemon');
        const data = await resp.json();
        this.setState({
            pokeLista: data.results
        })
        console.log('componentDidMount');
    }

    componentDidUpdate(prevProps, prevState){
        console.log('prevProps: ', prevProps, 'prevState: ', prevState)
        console.log('componentDidUpdate');
    }

    componentWillUnmount(){
        console.log('componentWillUnmount');
    }

    handlerLoadPokemons = async () => {
        const resp = await fetch('https://pokeapi.co/api/v2/pokemon');
        const data = await resp.json();
        this.setState({
            pokeLista: data.results
        })
    }

    handlerResetPokemons = () => {
        this.setState({
            pokeLista: []
        })
    }

    handlerUpdate = () => {
        this.forceUpdate()
    }

    render() {
        console.log('RENDER')
        return (
            <div>
                <h1>Lista Pokemon</h1>
                {
                  this.state.pokeLista.map(pokemon => 
                    <Fragment key={pokemon.name} >
                        <a href={pokemon.url} alt={pokemon.name + 'image'}> {pokemon.name} </a>
                        <p>{pokemon.url}</p>
                    </Fragment>
                  )
                }
                <button onClick={this.handlerLoadPokemons}>Load Pokemons</button>
                <button onClick={this.handlerResetPokemons}>Reset Pokemons</button>
                <button onClick={this.handlerUpdate}>Force Update</button>
            </div>        
        );
    }
}

LifeCycleComponent.defaultProps = {
    defaultList: []
}

export default LifeCycleComponent;
```

#### Otros métodos menos comunes

getDerivedStateFromProps()

```js
static getDerivedStateFromProps(props, state)
```
    getDerivedStateFromProps se invoca justo antes de llamar al método de render, tanto en la montura inicial como en las actualizaciones posteriores. Debes devolver un objeto para actualizar el estado, o nulo para actualizar nada.

    Este método existe para casos de uso raros donde el estado depende de los cambios en props con el tiempo. Por ejemplo, puede ser util para implementar un componente <Transition> que compare su anterior hijo y el siguiente para decidir cual de los dos animar en la entrada y salida.

shouldComponentUpdate()

```js
shouldComponentUpdate(nextProps, nextState)
```

    Usa shouldComponentUpdate() para avisar a React si la salida de un componente no se ve afectada por el cambio actual en el estado o los accesorios. El comportamiento predeterminado es volver a procesar cada cambio de estado y, en la gran mayoría de los casos, debe confiar en el comportamiento predeterminado.

    shouldComponentUpdate() es invocado antes de renderizar cuando los nuevos accesorios o el estado están siendo recibidos. Por defecto es true. Este método no es llamado para el renderizado inicial o cuando forceUpdate() es usado.

    Este método sólo existe como optimización de rendimiento.


getSnapshotBeforeUpdate()

```js
getSnapshotBeforeUpdate(prevProps, prevState)
```

    getSnapshotBeforeUpdate() se invoca justo antes de que la salida renderizada más reciente se entregue, por ejemplo, al DOM. Permite al componente capturar cierta información del DOM (por ejemplo, la posición del scroll) antes de que se cambie potencialmente. Cualquier valor que se devuelva en este ciclo de vida se pasará como parametro al método componentDidUpdate().

    Este caso de uso no es común, pero puede ourrir en IUs como un hilo de chat que necesita manejar la posición del scroll de manera especial.

    Debe devolverse un valor instantáneo (o null).





### EJERCICIO: TODO LIST 3: El regreso

![img](../../assets/react/clase36/todo.jpeg) 

<br>


## Nuevas rutas en la aplicación:

<br>

- `"/"`: Mostrará una vista de inicio, que de la bienvenida al usuario. Podremos agregar un botón que redirija al usuario a la sección `Lista de tareas`
- `/todo`: En esta vista tendremos acceso a las funcionalidades principales de la app (añadir tareas a una lista a través de un input de texto, borrar tareas individualmente, borrar todas las taresas)
- `/weather`: En esta vista tendremos acceso a la información del pronóstico del tiempo extendido (de las próximas 5 horas), en la ubicación donde se encuentre el usuario.



<br>
<br>

## Requisitos:

<br>

## `Para todas las vistas:` 
- Añadir una **Barra de Navegación** que permita acceder a las distintas rutas de la aplicación
- **Componente Footer** que mostrará los datos del clima actuales.

<br>
<br>

## `/todo` --> Vista TODO LIST :

<br>

- Un formulario con input + botón
- Un **componente List** que recorra una lista de items
- Un **componente Item o Card** que contenga cada TO DO
- Botón CLEAR para borrar todas las tareas
- Botón BORRAR, asociado a cada tarea, para poder borrar de manera independiente
- Botón para hacer RESET de las tareas
- Dar estilo CSS a los componentes con lo visto en clase para practicar

### Flujo de esta vista: 
- Hasta que no haya texto no aparecerá el botón ADD
- Si hemos escrito algo en el input y hacemos click sobre el botón ADD, se añadirá un item debajo del input.
- Cuando un item sea añadido, se borrará inmediatamente lo que habíamos escrito en el input y desaparecerá el botón ADD.
- Se debe hacer una precarga de tareas de un JSON de datos
- El botón de RESET mostrará de nuevo sólo las tareas obtenidas de la precarga de datos
- la precarga de datos se debe hacer usando el lifecycle
- Si pasados 20 segundos no envias la tarea que has escrito, se vaciará el input y desaparecerá ADD
- Cuando haya sido añadida una tarea se mostrará durante 5 segundos el mensaje "tarea añadida" y luego desaparecerá
- Validación: La tarea introducida en el input debe tener al menos 6 caracteres. En caso contrario debe aparecer un mensaje de error

<br>
<br>

## `/weather` --> Vista WEATHER INFO :

<br>

- Un **Componente WeatherList** que recorra una lista de items con la información del pronósitoc extendido de los próximos días. 
- Un **Componente WeatherCard** que contenga la información meteorológica de las próximas 5 horas (horario, temperatura, estado del tiempo (ej: clear, clouds, rain))
- Un formulario con input + botón para buscar una ciudad en concreto.

### Flujo de esta vista: 
- En esta vista se mostrará por defecto el pronóstico extendido de Madrid. Al introducir una nueva ciudad en el input de tipo texto y hacer click en el botón, la información se actualizará con los datos correspondientes a la ciudad buscada. 
- *EXTRA 1:* Agregar al componente una imagen que ilustre el estado del tiempo de cada día.
- *EXTRA 2:* En la primera carga de datos de esta vista, reemplazar Madrid por la geolocalización actual del usuario. 

<br>
<br>

TIP: usad el paquete de NPM UUID para manejar las keys de los diferentes elementos de la lista.
- [UUID](https://www.npmjs.com/package/uuid)
- [Sobre formularios](https://es.reactjs.org/docs/forms.html)


