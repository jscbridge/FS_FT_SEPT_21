![logotipo de The Bridge](https://user-images.githubusercontent.com/27650532/77754601-e8365180-702b-11ea-8bed-5bc14a43f869.png  "logotipo de The Bridge")
# [Bootcamp Web Developer Full Stack](https://www.thebridge.tech/bootcamps/bootcamp-fullstack-developer/)
### JS, ES6, Node.js, Frontend, Backend, Express, React, MERN, testing, DevOps



## Clase 36

### React(III): Form handling, event handling, refs

![img](../../assets/react/clase36/react.png)

### Formularios
- [Forms | ReactJS](https://es.reactjs.org/docs/forms.html) 
- [get-input-field-value-button-click-reactjs](https://therichpost.com/get-input-field-value-button-click-reactjs/)
- [how-to-get-input-text-value-on-click-in-reactjs](https://stackoverflow.com/questions/38443227/how-to-get-input-text-value-on-click-in-reactjs)


### Creando referencias: React.createRef()
- [working-with-refs-in-react](https://css-tricks.com/working-with-refs-in-react/)
- [ReactJS | refs-and-the-dom](https://es.reactjs.org/docs/refs-and-the-dom.html)

### EJERCICIO: TODO LIST

![img](../../assets/react/clase36/todo.jpeg) 

Crea una TODO list que contenga lo siguiente:

- Un formulario con input + botón
- Un componente List que recorra listas de items
- Un componente Item o Card que contenga cada TO DO
- Botón CLEAR para borrar todas las tareas
- Botón BORRAR, asociado a cada tarea, para poder borrar de manera independiente
- Botón para hacer RESET de las tareas
- Dar estilo CSS a los componentes con lo visto en clase para practicar

Flujo de la aplicación:
- Nada más empezar tendremos un input y un botón. El botón tendrá el texto ADD 
- Si hemos escrito algo en el input y hacemos click sobre el botón ADD, se añadirá un item debajo del input.
- Cuando un item sea añadido, se borrará inmediatamente lo que habíamos escrito en el input.
- Se debe hacer una precarga de tareas de un JSON de datos
- El botón de RESET mostrará de nuevo sólo las tareas obtenidas de la precarga de datos

TIP: usad el paquete de NPM UUID para manejar las keys de los diferentes elementos de la lista.
- [UUID](https://www.npmjs.com/package/uuid)
- [Sobre formularios](https://es.reactjs.org/docs/forms.html) 