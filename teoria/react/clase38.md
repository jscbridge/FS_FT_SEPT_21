![logotipo de The Bridge](https://user-images.githubusercontent.com/27650532/77754601-e8365180-702b-11ea-8bed-5bc14a43f869.png  "logotipo de The Bridge")
# [Bootcamp Web Developer Full Stack](https://www.thebridge.tech/bootcamps/bootcamp-fullstack-developer/)
### JS, ES6, Node.js, Frontend, Backend, Express, React, MERN, testing, DevOps


## Clase 38

### React(V): Comunicación entre componentes.Context

![img](../../assets/react/clase34/react.png)


### Comunicación entre componentes

![img](../../assets/react/clase38/drilling.png)

- [component-communication](https://www.javascriptstuff.com/component-communication/)
- [react-communicating-between-components](pluralsight.com/guides/react-communicating-between-components)
- [React JS Pass data from input in Child to Parent](https://codepen.io/TingChe/pen/MZNVMB?editors=0010)

### Levantando el estado
- [Levantando el estado | ReactJS](https://es.reactjs.org/docs/lifting-state-up.html)
- [Boiling Verdict](https://codepen.io/gaearon/pen/WZpxpz?editors=0010)
- [Demo levantando estado](https://jsfiddle.net/mtyson/21fm7c6t)


### React Context - patrón observador

- [Context | ReactJS](https://es.reactjs.org/docs/context.html)

- [manejo-de-estado-con-context-y-hooks-en-react](https://medium.com/noders/manejo-de-estado-con-context-y-hooks-en-react-7adfc7a740a3)
- [How to use the new React context API](https://hackernoon.com/how-to-use-the-new-react-context-api-fce011e7d87)
- [react-manage-user-login-react-context](https://www.digitalocean.com/community/tutorials/react-manage-user-login-react-context)
- [react-context-in-5-minutes](https://www.freecodecamp.org/news/react-context-in-5-minutes/)
- [Demo react context](https://codepen.io/kidkkr/pen/zXaEOp?editors=1010)

### EJERCICIO: Formulario + comunicación entre componentes

Crea un formulario + botón con los campos:
- Nombre
- Email
- URL foto
- Edad

Componentes:
- Head: Muestra el email del usuario registrado por el formulario
- Formulario: form + botón. Recibe datos de usuario
- Card. muestra los datos recibidos por el formulario

Comunicación:
- Head ha de leer por context el email del usuario
- Card y Formulario han de comunicarse en modo Sibling --- Sibling

