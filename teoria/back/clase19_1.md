![logotipo de The Bridge](https://user-images.githubusercontent.com/27650532/77754601-e8365180-702b-11ea-8bed-5bc14a43f869.png  "logotipo de The Bridge")


# [Bootcamp Web Developer Full Stack](https://www.thebridge.tech/bootcamps/bootcamp-fullstack-developer/)
### JS, ES6, Node.js, Frontend, Backend, Express, React, MERN, testing, DevOps

# Ejemplo básico Express.js

Aunque profundizaremos en el uso de Express.js, necesitamos ver un ejemplo básico para poder comunicar nuestro Back-end y Front-end de manera sencilla.

Express es un framework que permite gestionar peticiones y realizar enrutamiento de una menera más sencilla que lo que permite node solamente.

Veamos el ejemplo: 

### Index con form y post

```html
<!DOCTYPE html>
<html lang="es">
  <head>
    <title>Node JS Express Form Submission Example</title>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css">
  </head>
  <body>
    <div class="container">
      <h1>Node JS Express Form </h1>
      <form action="/" method="POST">
        <div class="form-group">
          <label for="firstName">First Name</label>
          <input type="text" class="form-control" id="firstName" aria-describedby="emailHelp" placeholder="Enter first name" name="first_name">
        </div>
        <div class="form-group">
          <label for="lastName">Last Name</label>
          <input type="text" class="form-control" id="lastName" aria-describedby="emailHelp" placeholder="Enter last name" name="last_name">
        </div>
        <div class="form-group">
          <label for="exampleInputEmail1">Email address</label>
          <input type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" name="email" placeholder="Enter email">
        </div>
        <button type="submit" class="btn btn-primary">Submit</button>
      </form>
  </body>
</html>
```

### Código Node usando Express
Antes de continuar debemos instalar express y body-parser en el directorio de nuestro proyecto: 

```javascript
  npm install express
  npm install body-parser
```

```javascript
const express = require('express');
const bodyParser = require('body-parser')
const app = express();
  
var urlencodedParser = bodyParser.urlencoded({ extended: false })
    
app.get('/', (req, res) => {
  res.sendFile(__dirname + '/index.html');
});
    
app.post('/', urlencodedParser, (req, res) => {
    console.log('First Name:', req.body.first_name, '\nLast Name: ', req.body.last_name, '\nEmail: ', req.body.email);
    res.send(req.body);
});
    
app.listen(3000);
```
### Ejercicio

1. Prueba la ejecución del ejemplo anterior construyendo un paquete npm y usando la opción start.
