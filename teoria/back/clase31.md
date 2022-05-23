![logotipo de The Bridge](https://user-images.githubusercontent.com/27650532/77754601-e8365180-702b-11ea-8bed-5bc14a43f869.png  "logotipo de The Bridge")


# [Bootcamp Web Developer Full Stack](https://www.thebridge.tech/bootcamps/bootcamp-fullstack-developer/)
### JS, ES6, Node.js, Frontend, Backend, Express, React, MERN, testing, DevOps

## Clase 31

### Testing E2E con Cypress + JSDOC


### Test de Integración

>Pruebas integrales o pruebas de integración son aquellas que se realizan en el ámbito del desarrollo de software una vez que se han aprobado las pruebas unitarias y lo que prueban es que todos los elementos unitarios que componen el software, funcionan juntos correctamente probándolos en grupo. Se centra principalmente en probar la comunicación entre los componentes y sus comunicaciones ya sea hardware o software.[Wikipedia](https://es.m.wikipedia.org/wiki/Prueba_de_integraci%C3%B3n)

![img](../../assets/back/clase31/unit_vs_integration.gif) 

![img](../../assets/back1/clase31/unit_integration_test.jpeg)         
- [tipos-de-testing-en-js](https://medium.com/@anamartinezaguilar/tipos-de-testing-en-js-89cd1c4507bf)


### Test E2E con Cypress

Los tests de aceptación o tests end-to-end son un tipo especial de tests de integración y tests funcionales que comprueban el resultado último de la aplicación y que se basan en los criterios definidos por el cliente. Por ejemplo, “que un usuario pueda crear una tarea nueva en nuestra aplicación de gestión de tareas”.

![img](../../assets/back/clase31/e2e_meme.jpg)

![img](../../assets/back/clase31/cypress.jpg)


Ejemplos:
- [Tutorial cypress](https://www.valentinog.com/blog/cypress/)
- [e2e-testing-in-node-js-using-cypress-io](https://cloudnweb.dev/2019/04/e2e-testing-in-node-js-using-cypress-io/)
- [Writing Your First Test - pagina cypress](https://docs.cypress.io/guides/getting-started/writing-your-first-test.html#Add-a-test-file)
- [testing-e2e-con-cypress-tutorial](https://tecnops.es/testing-e2e-con-cypress-tutorial-1-parte/)
- [cypress-un-framework-de-pruebas-todo-en-uno](https://www.paradigmadigital.com/dev/cypress-un-framework-de-pruebas-todo-en-uno/)


### Ejercicio E2E con Cypress
Vamos a hacer una demo para probar test E2E con Cypress
- [Tutorial cypress](https://www.valentinog.com/blog/cypress/)

### JSDOC

![img](../../assets/back/clase31/jsdoc.jpg)

JSDoc es una sintaxis para agregar documentación de la API al código fuente de JavaScript -[Wikipedia](https://es.wikipedia.org/wiki/JSDoc) 

#### Pasos a seguir: 

1. Instalar el paquete de JSDOC. Lo puedes instalar de forma global o como una dev-dependencies.

        npm install -g jsdoc

        npm install --save-dev jsdoc

2. Generamos un json de configuración en la carpeta principal. 

 `jsdoc.json`: 

 ```json
{
    "source": {
        "includePattern": ".+\\.js(doc|x)?$",   
        "include": ["."],                        
        "exclude": ["node_modules"]              
    },
    "recurseDepth": 10,                         
    "opts": {
        "destination": "./jsondocs/",          
        "recurse": true                         
}
```


3. Puedes añadir el siguiente comando en tu `package.json`. Esto te permitirá ejecutar el comando de forma más sencilla.

```json
"scripts": {
    "generate-docs": "jsdoc -c /path/to/my/conf.js"
}
```
4. ¡A documentar! 

La forma de documentar en JSdocs es agregar un comentario que comience con /** y finalice con */ sobre cada bloque que queramos comentar.

Al documentar podemos incluir diversas etiquetas que nos ayudarán a señalar los datos con los que estamos trabajando. Algunos ejemplos son los siguientes: 

- **@author** Sirve para indicar el autor de la documentación creada
-  **@exports** indica si hay alguna exportación en el documento
-  **@namespace** el nombre del objeto que se utiliza
-  **@memberof** a qué pertenece (objeto, función...)
-  **@method** el nombre de la función
-  **@param {}** el tipo de argumento que admite la función
-  **@return {}** el tipo de valor que devuelve.

5. Un ejemplo real: 

`products.js`
```javascript
/**
 * @author Silvia López <silvialopezpage.com> 
 * @exports routes 
 * @namespace routes 
 */
const routes = {
  /**
  * @memberof routes 
  * @method getEntries 
  * @async 
  * @param {Object} req 
  * @param {Object} res  
  * @return {json} 
  * @throws {error} 
  */
    getEntries: async (req, res) => {
        let email = req.query.email;
    
        try {
            const data = email? await Entry.getEntriesByEmail(email):await Entry.getAllEntries();
            res.status(200).json(data);
        } catch (err) {
        res.status(500).json({ message: err.message });
        }
    },
}

module.exports = routes
```

5. Puedes ejecutar el comando que has añadido en el package.json de la siguiente forma:
        
        npm run generate docs

Utilizando este comando generaremos la carpeta en la que aparecerá nuestra documentación en el archivo `index.html` de la carpeta a la que le hayamos indicado que lo genere. 

Podemos documentar todos nuestros archivos, sin embargo, dicho comando debe ejecutarse cuando ya esten documentados todos nuestros archivos a documentar, de lo contrario, en nuestro html solo aparecerá la información que se generó en el momento de ejecutar este comando.


#### Recursos

- [Guia para implementar JSDOC - Valentino](https://www.valentinog.com/blog/jsdoc/)
- [Guia para implementar JSDOC - dev.to](https://dev.to/paulasantamaria/document-your-javascript-code-with-jsdoc-2fbf)
- [Guia para implementar JSDOC - Spreaking.js](https://dev.to/paulasantamaria/document-your-javascript-code-with-jsdoc-2fbf)
- [Documentación oficial de jsdoc](https://jsdoc.app/tags-example.html)
- [Chuleta de JSDOC](https://devhints.io/jsdoc)








