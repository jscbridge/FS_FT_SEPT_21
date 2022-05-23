![logotipo de The Bridge](https://user-images.githubusercontent.com/27650532/77754601-e8365180-702b-11ea-8bed-5bc14a43f869.png  "logotipo de The Bridge")


# [Bootcamp Web Developer Full Stack](https://www.thebridge.tech/bootcamps/bootcamp-fullstack-developer/)
### JS, ES6, Node.js, Frontend, Backend, Express, React, MERN, testing, DevOps

## Clase 5

**HTML5: Web Storage**

Web Storage es la nueva caracteristica que traen los navegadores actuales gracias a HTML5 para guardar información en el lado del cliente. 

La información la guardamos al igual en pares clave-valor. Todo lo guardado resulta ser una cadena y la información es persistente sólo el lado del cliente.

Uso y limitaciones:
- 5-10Mb según navegador
- Almacenamiento local (lectura/escritura cliente)
- Sin caducidad
- Funcionamiento clave/valor
- Solo se permite el almacenamiento de cadenas de texto.

**Local Storage vs Session Storage**
- Local Storage no tiene fecha de expiración
- Session Storage solo será válida para la ventana actual en la que estamos navegando y solo son accesibles para el dominio actual. 
- La información de ambas puede ser eliminada si se limpia la información guardada en el navegador.

Recursos
- [MDN | API_de_almacenamiento_web](https://developer.mozilla.org/es/docs/Web/API/API_de_almacenamiento_web)
- [html-5-diferencias-y-ejemplos-entre-local-storage-y-session-storage](https://anexsoft.com/html-5-diferencias-y-ejemplos-entre-local-storage-y-session-storage)
- [que-es-y-como-utilizar-localstorage-y-sessionstorage](https://ed.team/blog/que-es-y-como-utilizar-localstorage-y-sessionstorage)
- [LocalStorage, sessionStorage](https://javascript.info/localstorage)
- [storing_and_retrieving_an_array_from_local_storage](https://www.kirupa.com/html5/storing_and_retrieving_an_array_from_local_storage.htm)

**Guardar datos**
```javascript
localStorage.setItem('name', 'Alejandro') // op1
localStorage.surname = 'Reyes' // op2
```

**Leer datos**
```javascript
let firstName = localStorage.getItem('name');
let lastName  = localStorage.surname;
console.log(`Hola, mi nombre es ${firstName} ${lastName}`)
```

**eliminar datos**
Se borra por clave
```javascript
localStorage.removeItem('surname')
```

**borrar todo**
```javascript
localStorage.clear()
```

**Leer todo lo que hay en local Storage**
```javascript
for(let i=0; i<localStorage.length; i++) {
  let key = localStorage.key(i);
  alert(`${key}: ${localStorage.getItem(key)}`);
}
```

**Leer/escribir un objeto de LocalStorage**

usar JSON.stringify() y JSON.parse()
- [MDN | JSON.stringify()](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/JSON/stringify)
- [MDN | JSON.parse()](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/JSON/parse)

```javascript
//Escribir
localStorage.setItem('user', JSON.stringify({
    username: 'Alejandro',
    api_key: 'abc123xyz789'
}));
//Leer
var user = JSON.parse(localStorage.getItem('user'));
```

**Leer/escribir un array de LocalStorage**
```javascript
var movies = ["Reservoir Dogs", "Pulp Fiction", "Jackie Brown", 
              "Kill Bill", "Death Proof", "Inglourious Basterds"];
//Escribir
localStorage.setItem("quentinTarantino", JSON.stringify(movies));

//Leer
var retrievedData = localStorage.getItem("quentinTarantino");
```

**Object Methods**
- [MDN | Objects](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Object) 
- [how-to-use-object-methods-in-javascript](https://www.digitalocean.com/community/tutorials/how-to-use-object-methods-in-javascript)

- Object.entries()
```javascript
// Initialize an object
const operatingSystem = {
    name: 'Ubuntu',
    version: 18.04,
    license: 'Open Source'
};

// Get the object key/value pairs
const entries = Object.entries(operatingSystem);

console.log(entries);
/*
[
    ["name", "Ubuntu"]
    ["version", 18.04]
    ["license", "Open Source"]
]
*/
```

- Object.keys()
```javascript
// Initialize an object
const employees = {
    boss: 'Michael',
    secretary: 'Pam',
    sales: 'Jim',
    accountant: 'Oscar'
};

// Get the keys of the object
const keys = Object.keys(employees);
console.log(keys);//["boss", "secretary", "sales", "accountant"]
```
- Object.values()
```javascript
// Initialize an object
const session = {
    id: 1,
    time: `26-July-2018`,
    device: 'mobile',
    browser: 'Chrome'
};

// Get all values of the object
const values = Object.values(session);

console.log(values); // [1, "26-July-2018", "mobile", "Chrome"]
```
- Object.create()
```javascript
// Initialize an object with properties and methods
const job = {
    position: 'cashier',
    type: 'hourly',
    isAvailable: true,
    showDetails() {
        const accepting = this.isAvailable ? 'is accepting applications' : "is not currently accepting applications";

        console.log(`The ${this.position} position is ${this.type} and ${accepting}.`);
    }
};

// Use Object.create to pass properties
const barista = Object.create(job);

barista.position = "barista";
barista.showDetails();
```

- Object.assign()
```javascript
// Initialize an object
const name = {
    firstName: 'Philip',
    lastName: 'Fry'
};

// Initialize another object
const details = {
    job: 'Delivery Boy',
    employer: 'Planet Express'
};

// Merge the objects
const character = Object.assign(name, details);
console.log(character);
```


### Ejercicios

#### 1. Formulario de contacto - Local Storage
- Crear un formulario de contacto con los siguientes campos:
  - Nombre
  - Email
  - Mensaje
- Guardar en Local Storage los datos de contacto enviados de cada usuario
- Mostrar los datos de los contactos guardados en el DOM
- Usa `JSON.parse()` y `JSON.stringify()` para guardar muchos datos usando la misma clave

#### 2. Avanzado - Local Storage
- Crea botón para borrar todos los contactos guardados en Local Storage
- Crea botón para borrar un contacto en concreto de Local Storage.