![logotipo de The Bridge](https://user-images.githubusercontent.com/27650532/77754601-e8365180-702b-11ea-8bed-5bc14a43f869.png  "logotipo de The Bridge")
# [Bootcamp Web Developer Full Stack](https://www.thebridge.tech/bootcamps/bootcamp-fullstack-developer/)
### JS, ES6, Node.js, Frontend, Backend, Express, React, MERN, testing, DevOps


## Clase 40

### React: Ejercicio

## Vamos a picar código!!
![img](../../assets/react/clase40/code.gif)


### EJERCICIO: Página de noticias
![img](../../assets/react/clase40/newsmeme.jpg)

Vamos a englobar todo lo visto estos días con un miniproyecto con React

- [News API](https://developer.nytimes.com/apis) 

Routing
- `/home`. Home de la app
- `/form`. Formulario para crear noticia
- `/list`. Lista detallada de noticias

Componentes mínimos (Te toca a tí ordenar el arbol de componentes :smile: )
- `Head`
- `Nav`
- `Main`
- `Home`. Input + botón para introducir nombre de usuario
- `Form`. Formulario de alta de nueva noticia. Tras dar de alta debes redirigir a ListNews
- `ListNews`. Haz una precarga de 5 noticias de la API + las que has dado de alta. Tu eliges el topic
- `Card`. Representa cada noticia. Debe tener un botón para poder borrarla
- `Footer`

Comunicación
- Context:
    - Se debe introducir nombre de usuario desde la Home. Provider
	- En el Head debe aparecer el nombre de usuario. Consumer
- Sibling--sibling. Para Form y ListNews

CSS/SCSS. Utilizar las técnicas de estilo vistas en clase

Lifecycle: No olvides usarlo para el tema de llamadas asíncronas

NOTA: Si necesitas añadir algún componente más, feel free!
