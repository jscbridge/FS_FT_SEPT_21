![logotipo de The Bridge](https://user-images.githubusercontent.com/27650532/77754601-e8365180-702b-11ea-8bed-5bc14a43f869.png  "logotipo de The Bridge")
# [Bootcamp Web Developer Full Stack](https://www.thebridge.tech/bootcamps/bootcamp-fullstack-developer/)
### JS, ES6, Node.js, Frontend, Backend, Express, React, MERN, testing, DevOps

## Clase 45
**Testing en React**

![img](../../assets/react/clase45/cat.jpg) 

### JEST Y REACT


La librería `@testing-library` nos ayuda a testear los componentes de la UI de nuestra app centrándonos en el usuario. 

Los proyectos creados con create-react-app ya traen soporte para trabajar con **React Testing Library**.

En el fichero *package.json* podemos ver incluídas las dependencias necesarias para trabajar con la librería. 

```JS
    "@testing-library/jest-dom": "^5.14.1"
    "@testing-library/react": "^11.2.7"
    "@testing-library/user-event": "^12.8.3"
```
 
Allí también encontraremos el script para ejecutar el test con **React Testing Library**
```JS
    "test": "react-scripts test"
```

Lo primero que haremos será importar la función `render` y el objeto `screen`

```JS
    import { render, screen } from '@testing-library/react';
```

Para testear componentes, debemos importarlos del mismo modo en el que lo hacemos en otros ficheros de nuestra aplicación.

```JS
    import App from './App.js'
```

En el archivo `App.test.js` ya tenemos un primer test unitario que evalúa el correcto funcionamiento del script que trae por defecto el fichero `App.js`

Por cada componente creamos un fichero `.test.js` en la misma carpeta que el fichero del componente y escribimos sus tests allí.

Tests de ejemplo

1. Comprobamos que sea visible 
```JS
test('Learn React link is visible', () => {
  render(<App />);
  const linkElement = screen.queryByText('Learn React');
  expect(linkElement).toBeVisible();
});
```
2. Comprobamos que esté en el DOM sin importar su visibilidad con `.toBeInTheDocument()`
```JS
 test('Learn React link is redered', () => {
  render(<App />);
  const linkElement = screen.getByText(/learn react/i);
  expect(linkElement).toBeInTheDocument();
});
```
3. Comprobamos el atributo de un elemento con `.toHaveAttribute(clave, valor)`
```JS
 test('Learn React link has href', () => {
  render(<App />);
  const linkElement = screen.getByText(/learn react/i);
  expect(linkElement).toHaveAttribute('href', 'https://reactjs.org');
});
```
4. Con `queryAllByText` capturo una colección de nodos y con `expect(miColeccionDeNodos.length).toBe(number)` compruebo su longitud, que es equivalente a comprobar cuántos hay.
```JS
 test('List has 4 list items', () => {
  render(<App />);
  const list = screen.getAllByText(/item/i);
  expect(list.length).toBe(4);
});
```
5. Comprobamos que tenga determinada clase con .toHaveClass(nombreDeLaClase)
```JS
 test('List items have className item', () => {
  render(<App />);
  const list = screen.getAllByText(/item/i);
  list.forEach((li)=>{
    expect(li).toHaveClass('item');
  })
});
```
6. Simulamos el disparo de un evento para comprobar que el resultado es el buscado con `await fireEvent.click(boton)`
```JS
 test('Button to show and hide text', async () => {
  render(<App />);
  const button = screen.getByTestId('btn');
  await fireEvent.click(button)
  const text = screen.getByTestId('text')
  expect(text).toBeVisible()
});
```


- [Jest y React | Testing the DOM](https://jestjs.io/docs/es-ES/next/tutorial-react)


<!-- **DOM Testing** 
> If you'd like to assert, and manipulate your rendered components you can use react-testing-library, Enzyme, or React's TestUtils. The following two examples use react-testing-library and Enzyme. -->

### React-testing-library

- [Documentación oficial de React-testing-library](https://github.com/testing-library/react-testing-library)

- [Demo para testear botones](https://flaviocopes.com/react-testing-components/)

- [Demo para testear componentes](https://testing-library.com/docs/react-testing-library/migrate-from-enzyme/)

- [Testear partes de tu APP en React](https://codesandbox.io/s/github/kentcdodds/react-testing-library-examples?file=/src/)

### Ejercicio

Testear el componente `App` y el componente `Card` de nuestra **PokeApp**

Los requisitos que el test tendrá que cubrir son:

- Que `App` sea visible

- Que en `App` sea visible un elemento con la *clase "App__btn" o "App__input"*

- Que diAppcho elemento contenga el *texto "buscar"*

- Que en `App` sea visible un elemento con el *testId "App__inputText"*

- Que dicho elemento contenga un *placeholder* con el string "Introduce un Pokemon"

- Que `Card` sea visible

- Que `Card` contenga un elemento con el *testId "Card__title"*

- Que `Card` contenga un elemento con el *testId "Card__img"*

- Que cuando `Card` reciba por **props** un objeto con los campos "name" y "sprites.front_default" el valor de *name* sea visible en un elemento con el *testId "Card__title"*

- Que el valor del campo "sprites.front_default" exista en el *atributo src del elemento "Card__img"*

