![logotipo de The Bridge](https://user-images.githubusercontent.com/27650532/77754601-e8365180-702b-11ea-8bed-5bc14a43f869.png  "logotipo de The Bridge")


# [Bootcamp Web Developer Full Stack](https://www.thebridge.tech/bootcamps/bootcamp-fullstack-developer/)
### JS, ES6, Node.js, Frontend, Backend, Express, React, MERN, testing, DevOps

## Clase 23

### Express(III): Fetch + Middlewares

![img](../../assets/back/clase23/express.png)

### Peticiones a APIs externas. Fetch con Express
- [node-fetch](https://www.npmjs.com/package/node-fetch )
- [Github | node-fetch](https://github.com/node-fetch/node-fetch)
- [using-async-await-in-express-with-node](https://medium.com/@Abazhenov/using-async-await-in-express-with-node-8-b8af872c0016)
- [making-http-requests-in-node-js-with-node-fetch]( https://stackabuse.com/making-http-requests-in-node-js-with-node-fetch/)

### Middlewares 
- [Express | using-middleware](https://expressjs.com/es/guide/using-middleware.html)
- [middleware-en-express-js](https://medium.com/@aarnlpezsosa/middleware-en-express-js-5ef947d668b)
- [logging-in-a-node-express-app-with-morgan-and-bunyan](https://medium.com/@tobydigz/logging-in-a-node-express-app-with-morgan-and-bunyan-30d9bf2c07a)
- [Morgan](https://www.npmjs.com/package/morgan)
- [body-parser](https://apuntes.de/nodejs-desarrollo-web/body-parser/#gsc.tab=0)
- [CORS](https://riptutorial.com/es/node-js/example/28740/habilitar-cors-en-express-js)

### Manejo de 404 Not found - Crear un Middleware propio
- [how-to-handle-404-error-in-express](https://techeplanet.com/how-to-handle-404-error-in-express/)



### EJERCICIO -  Server Render con Express + Pug

![img](../../assets/back/clase23/pug_meme.jpeg)

Crea una aplicación de películas para hacer server render con Nodejs y Pug. Para ello usa la API de pelis que te proporcionamos
- [OMDB api](http://www.omdbapi.com/)
Templates:
- `home.pug` --> Renderiza un formulario de búsqueda por título de película
- `film.pug` --> Renderiza los detalles de una película: título, autor, descripción, imagen...

Rutas:
- [GET] `http://localhost:3000` Home de la app. Se renderiza home.pug
- [GET] `http://localhost:3000/film/:title` Muestra los datos de una peli por título. Internamente se hace un fetch a la API de pelis para obtener dichos datos. Debe renderizar film.pug
- [POST] `http://localhost:3000/film/` Se envía el POST a esta ruta cuando envías el formulario de búsqueda de peli de `home.pug`. Puede ser de ayuda usar `res.redirect()`

