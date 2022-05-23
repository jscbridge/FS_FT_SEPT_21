![logotipo de The Bridge](https://user-images.githubusercontent.com/27650532/77754601-e8365180-702b-11ea-8bed-5bc14a43f869.png  "logotipo de The Bridge")
# [Bootcamp Web Developer Full Stack](https://www.thebridge.tech/bootcamps/bootcamp-fullstack-developer/)
### JS, ES6, Node.js, Frontend, Backend, Express, React, MERN, testing, DevOps


## Clase 42

### React: Componentes funcionales. Hooks(II)
![img](../../assets/react/clase40/hooksmeme.jpg)

### Hooks 
- [hooks-overview | ReactJS](https://es.reactjs.org/docs/hooks-overview.html)
- [react-hooks-para-principiantes](https://medium.com/@mariasolahornedo/react-hooks-para-principiantes-dfb659cc7209)

<br>

### **Hooks: `useContext()`**

<br>

`useContext()` acepta un objeto de contexto (el valor devuelto de React.createContext) y devuelve el valor de contexto actual. El valor actual del contexto es determinado por la propiedad value del `<MyContext.Provider>`.

El argumento enviado a **useContext** debe ser el objeto del contexto en sí mismo.

Un componente que llama a **useContext** *siempre se volverá a renderizar* cuando el valor del contexto cambie..

`useContext(MyContext)` es el equivalente a `static contextType = MyContext` en una clase, o a `<MyContext.Consumer>`.

- ***useContext(MyContext)** solo te permite leer el contexto y suscribirte a sus cambios. Aún necesitas un **<MyContext.Provider>** arriba en el árbol para proveer el valor para este contexto.*

### Ejemplo práctico: 

- Añadiremos un botón en nuestro componente `Footer` que modifique el color de fondo de nuestro componente `Counter`

1. Crear un botón en el **Footer** de nuestra aplicación cuya función será cambiar el color de fondo de nuestro componente `Counter`
2. Añadir un @mixin dark-theme() en el fichero `_mixins.scss` 
```CSS
@mixin dark-theme(){
    background-color: black;
    box-shadow: 4px 4px 24px grey
}
```
3. Crear una clase de nombre 'dark' en nuestro fichero `App.scss`
```CSS
.dark{
  @include dark-theme()
}
```

4. Crear **el context** con un valor por defecto (en este caso *null*) en un fichero `themeContext.js` y guardarlo en nuestra carpeta *context*

```JS
import React from 'react'
export const ThemeContext = React.createContext(null)
```

5. Importar **useContext** en `App.js`, `Footer.js` y `Counter.js`
```JS
import { useContext } from 'react'
```

6. Importar el **contexto** con el que vamos a trabajar en cada componente
```JS
import { ThemeContext } from './context/themeContext'
```

7. Agregar el Provider en `App.js` envolviendo los componentes que trabajarán con el contexto (tal cual lo hacemos en React de clases). En el atributo *value* pasaremos el objeto con los valores del context que necesitamos (estados o funciones)
```JS

const theme = {
    theme: this.state.theme,
    toggleTheme: this.toggleTheme
}
///...
<ThemeContext.Provider value={theme}> 
   /// componentes que utilizarán ThemeContext
</ThemeContext.Provider>
```

8. Ejecutar **useContext** pasándole el contexto que queremos utilizar en aquellos componentes que consuman dicho context. 
Almacenar el valor de **useContext** en una variable (podemos hacer destructuring de dicho objeto)
```JS
const { theme, toggleTheme } = useContext(ThemeContext)
```

9. Ahora solo nos queda trabajar con los estados y funciones del context creado en los componentes que lo consuman. Por ejemplo, para añadir una clase al div contendor de `Counter.js`:

```JS
return (
    <div className={`Counter ${theme}`}>
        {/*...*/}
    </div>
);
```

<br>
<br>

Documentación:

<br>

- [hooks-reference | ReactJS](https://es.reactjs.org/docs/hooks-reference.html)
- [usecontext-hook](https://daveceddia.com/usecontext-hook/)
- [react-usecontext](https://www.digitalocean.com/community/tutorials/react-usecontext)

<br>
<br>

### **Custom Hooks**

<br>

Los **custom hooks** son funciones de JavaScript cuyo nombre comienza por `use` y pueden a su vez llamar a otros hooks de React.
Permiten extraer la lógica de un componente y encapsularla en funciones reutilizables.

### Ejemplo práctico: 

- Refactorizaremos el componente de clase `Staff` a un componenete funcional y encapsularemos el fetch a la Api en un custom hook que guardaremos en una **carpeta hooks** con el nombre `useFetch`.
El hook `useFetch` devolverá una variable *loading* (booleano) y una variable *result* con la respuesta de la api. 


useFetch
```JS
import { useState, useEffect } from 'react';
import axios from 'axios'

// useFetch será una función que reciba como parámetro un string con una url

const useFetch = (url) => {
    // Crearemos dos estados: loading(true) y result([]), que devolveremos en un objeto
    const [loading, setLoading] = useState(true)
    const [result, setResult] = useState([])

    // Añadiremos un useEffect que se ejecutará cuando la url cambie y hará un fetch a dicha url
    useEffect( async ()=>{
        try{
            const response = await axios.get(url)
            // vamos a agregar un setTimeout a continuación del fetch para apreciar mejor el comportamiento del hook
            // Dentro del setTimeout actualizaremos los dos estados de este hook (loading y result)
            setTimeout(() => {
                setResult(response.data)
                setLoading(false)
            }, 5000);
        } catch (err) {
            console.log(err)
        }      
    }, [url])
    
    return { loading, result }
}

// Haremos un export default de la función para importarla como hook en el componente deseado
export default useFetch;
```

<br>
<br>

- [react-custom-hooks](https://reactgo.com/react-custom-hooks/)

### Awesome Hooks
- [10-react-custom-hooks-you-should-have-in-your-toolbox](
https://blog.bitsrc.io/10-react-custom-hooks-you-should-have-in-your-toolbox-aa27d3f5564d)
- [awesome-react-hooks](https://github.com/rehooks/awesome-react-hooks)

### EJERCICIO: PokeApp con React Funcional (II)

![img](../../assets/react/clase39/Pokemon.jpg)

- [pokeapi](https://pokeapi.co/)

- Vamos a cambiar el estado que habíamos creado antes para almacenar un solo pokemon. Vamos a poner en su lugar una lista ([]).
- Ahora, cada vez que pulsemos el botón para buscar un pokemon, el pokemon encontrado deberá concatenarse a la lista que tenemos almacenada en el estado en lugar de almacenar uno solo.
- Crea el Componente ListaPokemon, que deberá dibujar una lista con todas las Card de datos e imagen del Pokemon.
- NOTA: El ejercicio se debe hacer con React funcional y como mínimo con los Hooks `useState()` y `useEffect()`.
- Para practicar, puedes investigar y hacer uso de cualquier otro Hook (tanto propio como de terceros) que tenga sentido para este ejercicio.



