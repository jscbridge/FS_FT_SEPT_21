![logotipo de The Bridge](https://user-images.githubusercontent.com/27650532/77754601-e8365180-702b-11ea-8bed-5bc14a43f869.png  "logotipo de The Bridge")
# [Bootcamp Web Developer Full Stack](https://www.thebridge.tech/bootcamps/bootcamp-fullstack-developer/)
### JS, ES6, Node.js, Frontend, Backend, Express, React, MERN, testing, DevOps



## Clase 39

### React: Componentes funcionales. Hooks

![img](../../assets/react/clase39/React-Hook.png)

### **Componentes de clase vs funcional**
- [functional-vs-class-components-in-react](
https://medium.com/@Zwenza/functional-vs-class-components-in-react-231e3fbd7108)
- [react-functional-vs-class-components](
https://medium.com/@amarchitelli1993/react-functional-vs-class-components-ac6b0c9e38bb)
- [react-choose-functional-components](
https://www.twilio.com/blog/react-choose-functional-components)
- [functional-components-vs-class-components-in-react](
https://www.freecodecamp.org/news/functional-components-vs-class-components-in-react/)
- [react-preference-function-class-vs-component-class](
https://stackoverflow.com/questions/61859809/react-preference-function-class-vs-component-class)



### **Hooks** 

**Los Hooks son funciones** que permiten trabajar con **estados** y **ciclo de vida** en componentes funcionales. 
Los hooks no funcionan dentro de las clases.

React proporciona algunos Hooks incorporados como **useState** y **useEffect**, pero también existe la posibilidad de crear **tus propios Hooks** para reutilizar en distintos componentes. 

Los Hooks son una nueva característica que se incorpora en la versión React 16.8 (febrero 2019). 

**Ventajas:**

- Ya no es necesario que el estado del componente sea un objeto. Podemos utilizar valores primitivos (string, number, boolean)
- Prescindimos del uso de <span style="color: #547AEF; font-weight: bolder">this</span> .
- Los alias del nuevo *state* hacen que el código sea más legible.
- El código luce sintácticamente más simple, legible y fácil de mantener. 
- Los Hooks se pueden compartir entre distintos componentes o incluso con la comunidad.
- La curva de aprendizaje de React con Hooks es mucho más rápida. 

Documentación: 

- [hooks-overview | ReactJS](https://es.reactjs.org/docs/hooks-overview.html)
- [react-hooks-para-principiantes](https://medium.com/@mariasolahornedo/react-hooks-para-principiantes-dfb659cc7209)


### **Hooks: `useState()`**

- [hooks-state](https://es.reactjs.org/docs/hooks-state.html)
- [usestate-hook-examples](https://daveceddia.com/usestate-hook-examples/)


**useState** es una función que toma el estado inicial como un argumento y devuelve *un array de dos elementos*. 

El primer elemento es una variable donde se almacena el **estado actual** y el segundo es una **función que actualiza dicho estado.** El valor que devuelva la función pasará a almacenarse en la variable o primer elemento del array. 



Vamos a ver un ejemplo de como usar el estado con useState en un componente funcional.
Partimos de un ejemplo sencillo de un contador con un componente de clase:

```js
import React, { Component } from 'react';

class HooksUseState extends Component {
  
    state = {
        count: 0
    }

    handleAddClick = () => {
        this.setState({
            count: this.state.count + 1
        })
    }

    handleSubClick = () => {
        this.setState({
            count: this.state.count - 1
        })
    }

    render() { 
        return (
            <>
                <button name='add' onClick={this.handleAddClick} >+</button>
                <h1>The value is: {this.state.count}</h1>
                <button name='sub' onClick={this.handleSubClick} >-</button>
            </>
        );
    }
}
 
export default HooksUseState
```

Ahora convirtamos este componente de clase con hooks y useState:

```js
import React, { useState } from 'react';

const HooksUseState = () => {
  
    const [count, setCount] = useState(0);
    // useState devuelve un array [state, ()setState]
    // asique usamos destructuring para sacarlos a variables

    const handleAddClick = () => {
        setCount(count + 1)
    }

    const handleSubClick = () => {
        setCount(count - 1)
    }

    return (
        <>
            <button name='add' onClick={handleAddClick} >+</button>
            <h1>The value is: {count}</h1>
            <button name='sub' onClick={handleSubClick} >-</button>
        </>
    );
    
}
 
export default HooksUseState
```

### useState con objetos 

Bien, anteriormente vimos el uso de useState con una variable numerica, los demas tipos de datos (string, boolean, etc) se tratan exactamente igual.

Vamos a ver un ejemplo usando useState con objetos:

```js
import React, { useState } from 'react';

const HooksUseStateObject = () => {
  
    const [values, setValues] = useState({
        email: '',
        password: ''
    });

    const handleChange = (e) => {
        setValues({
            ...values,
            [e.target.name]: e.target.value
        })
    }

    const handleSubmit = (e) => {
        e.preventDefault()
        console.log(values)
    }

    return (
        <>
            <form onSubmit={handleSubmit}>
                <label htmlFor="email">Email</label>
                <input name="email" type="text" onChange={handleChange}></input>
                <br/><br/>
                <label htmlFor="password">Password</label>
                <input name="password" type="text" onChange={handleChange}></input>

                <button>Login</button>
            </form>
            <p>{JSON.stringify(values)}</p>
        </>
    );
    
}
 
export default HooksUseStateObject
```

### DefaultProps con Hooks

Vimos anteriormente en los componentes de clase que podiamos declarar las defaultProps de la siguiente manera:

```js
HooksDefaultProps.defaultProps = {
    count: 100
}
```

Con Hooks es muy común inicializar las props como en el siguiente ejemplo:

```js
import React, { useState } from 'react';

const HooksUseState = ({initialCount = 10}) => {
  
    const [count = initialCount, setCount] = useState();
    // esta vez no le pasamos nada en el método useState
    // en el ejemplo anterior ----- useState(0)
    // en este ejemplo   ------ useState()

    const handleAddClick = () => {
        setCount(count + 1)
    }

    const handleSubClick = () => {
        setCount(count - 1)
    }

    return (
        <>
            <button name='add' onClick={handleAddClick} >+</button>
            <h1>The value is: {count}</h1>
            <button name='sub' onClick={handleSubClick} >-</button>
        </>
    ); 
}
 
export default HooksUseState
```



### **Hooks: `useEffect()`**

- [hooks-effect](https://es.reactjs.org/docs/hooks-effect.html)
- [useeffect-hook-examples](https://daveceddia.com/useeffect-hook-examples/)

**useEffect** nos permite ejecutar código cada vez que nuestro componente se renderiza o actualiza su estado. 

El ciclo de vida en React permite ejecutar código en diferentes fases del montaje, actualización y desmontaje de los componentes.

Con **useEffect** podemos controlar el ciclo de vida de *componentes funcionales* de una forma clara y sencilla.

**useEffect** es un hook que recibe como parámetro una función que se ejecutará cada vez que nuestro componente se renderice, ya sea por un cambio de estado, por recibir props nuevas o porque es la primera vez que se monta.

Importar **useEffect**
```js
import React, { useEffect } from 'react'
```
Inicializar **useEffect** para que se ejecute cada vez que el componente se renderice. 
```js
 useEffect( () => {
    console.log('render!')
  })
```

Por defecto **useEffect** se dispara cada vez que se realiza un nuevo renderizado.  Podemos evitar que el efecto se vuelva a ejecutar pasándole *un segundo parámetro* al hook. Este parámetro es *un array con todos los valores de los que depende nuestro efecto*, de forma que sólo se ejecutará cuando ese valor cambie.

Para ejecutar determinado código solo al montarse el componente, debemos añadir un array vacío como segundo parámetro de **useEffect**. 
```js
 useEffect( () => {
    console.log('render only when component mounts!')
  }, [])
```
* *Funciona de manera análoga a `componentDidMount()`*

Si queremos que se ejecute código específico al actualizarse uno o más estados del componente, debemos añadir como segundo parámetro un array que contenga dicho estado o estados. 
```js
 useEffect( () => {
    console.log('render when the state changes!')
  }, [someState])
```
* *Funciona de manera similar a `componentDidUpdate()`*


Si queremos que se ejecute código específico al desmontarse el componente, debemos añadir a la función del **useEffect()** un <span style="color: #87009c; font-weight:bold">return</span> que devuelva una función con el código a ejecutarse. 

```js
useEffect(() => {
    // función de callback para actualizar el estado con el clientWidth
    const updateWidth = () => {
      const width = document.body.clientWidth
      console.log(`updateWidth con ${width}`)
      setWidth(width)
    }
    // actualizaremos el width al montar el componente
    updateWidth()
    // nos suscribimos al evento resize de window
    window.addEventListener("resize", updateWidth)

    // devolvemos una función para anular la suscripción al evento
    return () => {
      window.removeEventListener("resize", updateWidth)
    }
  }, [])
```

* *Funciona de manera análoga a `componentWillUnmount()`*


Otros ejemplos de cómo podemos usarlo:

```js
import React, { useEffect, useState } from 'react';

const HooksUseEffectExample = () => {
  
    const [date, setDate] = useState(new Date().toLocaleTimeString());


    useEffect(() => {
        // componentDidMount
        console.log('MOUNTED')

        // componentDidUpdate
        const time = setInterval(() => setDate(new Date().toLocaleTimeString()),
        1000)

        // componentWillUnmount
        return () => {
            clearInterval(time)
        }
    })

    return (
        <h1>{date}</h1>
    );
    
}
 
export default HooksUseEffectExample
```

Como veis 'useEffect' recibe un callback como primer parámetro, tambien podemos pasarle un array como segundo parametro para indicarle que solo se ejecute cuando algún state ha cambiado, si le ponemos un array vacio '[]' solo se ejecutará en el montado del componente y no cuando se actualice el state.

Si le pasamos un state dentro del array por ejemplo '[pokemon]' este solo se ejecutará cuando el state pokemon cambie.

ejemplo:

```js
import React, { useEffect, useState } from 'react';

const HooksUseEffect = () => {
  
    const [pokemons, setPokemons] = useState([]);

    useEffect(() => {
        const getPokemons = async () =>{
            const resp = await fetch('https://pokeapi.co/api/v2/pokemon');
            const data = await resp.json();
            setPokemons(data);
        }
        getPokemons();
    }, []);

    return (
        <p>{JSON.stringify(pokemons)}</p>
    );
    
}
 
export default HooksUseEffect
```


### EJERCICIO: PokeApp con React Funcional (I)

![img](../../assets/react/clase39/Pokemon.jpg)

- [pokeapi](https://pokeapi.co/)

En este ejercicio  trabajaremos con React funcional y haremos uso de los Hooks `useState()` y `useEffect()`

En este ejercicio tendréis que jugar con la Pokeapi. Se dividirá en los siguientes pasos:
- Crea un input de texto.
- Crea un botón.
- Crea un componente **Card** en el que dibujaremos los datos del personaje obtenido
- Crea, con `useState`, dos estados: uno para input `('')` y otro para un pokemon `({})`.
- Cada vez que escribamos en el input, su contenido se deberá guardar en el estado del input.
- Cuando pulsemos el botón que hemos creado antes, se deberá hacer una petición a la PokeApi con el nombre o el número del pokemon correspondiente registrado en el estado del input.
- Si va bien, la PokeApi devolverá un objeto con el pokemon elegido. El estado del pokemon que hemos creado antes debe actualizarse con el nuevo pokemon.
- Se debe dibujar en Card los datos e imágen del Pokemon.
- ***Al actualizarse*** la información del componente Card, la búsqueda del input de texto debe borrarse/resetear su valor a `('')`

