![logotipo de The Bridge](https://user-images.githubusercontent.com/27650532/77754601-e8365180-702b-11ea-8bed-5bc14a43f869.png  "logotipo de The Bridge")


# [Bootcamp Web Developer Full Stack](https://www.thebridge.tech/bootcamps/bootcamp-fullstack-developer/)
### JS, ES6, Node.js, Frontend, Backend, Express, React, MERN, testing, DevOps

## CRUD MySQL con Nodejs
Vamos a realizar las operaciones básicas con los conocimientos que tenemos ya de MySQL y usando Nodejs.

Veamos paso a paso el script de prueba que vamos a usar en esta ocasión.

### Preparativos
1. Crea un proyecto nuevo para Node e instala en él la librería de MySQL: 

```javascript
    npm install mysql
```

2. Crea una BD para hacer tus pruebas, con una tabla, varios inserts iniciales para pruebas, un procedimiento y una función. La idea es usar todo esto como base para tu script en Node:

```sql
    #DROP DATABASE prueba;
    CREATE DATABASE prueba;
    USE prueba;
    CREATE TABLE tabla1(
        id INT AUTO_INCREMENT,
        campoTexto VARCHAR(100),
        PRIMARY KEY(id)
    ); 

    INSERT INTO tabla1 VALUES(NULL, "Valor 1 CampoTexto");
    INSERT INTO tabla1 VALUES(NULL, "Valor 2 CampoTexto");
    INSERT INTO tabla1 VALUES(NULL, "Valor 3 CampoTexto");

    #Procedimiento
    DELIMITER $$
    CREATE PROCEDURE todoTabla1()
    BEGIN
        SELECT * FROM tabla1;
    END$$
    DELIMITER ;

    CALL todoTabla1();

    #Funcion
    DELIMITER $$
    CREATE FUNCTION primerID() RETURNS INT DETERMINISTIC
    BEGIN
        DECLARE r INT;
        SELECT id INTO r FROM tabla1 LIMIT 1;
        RETURN r;
    END$$
    DELIMITER ;

    SELECT primerID();
    
    #ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'root';

```

3. Cambia la configuración de la contraseña de root en MySQL para poder acceder desde Node: 

```sql
    ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'root';
```

4. Crea un paquete npm para poder ejecutar con **npm start**

Pasemos ya al contenido del script por partes: 

### Primera parte: Inclusión de librería y constante para la conexión: 

```javascript
    const mysql = require('mysql');
    const connection = mysql.createConnection({
        host: 'localhost',
        user: 'root',
        password: 'root',
        database: 'prueba'
    });

```
### Segunda parte: Probar la conexión: 

```javascript
    
    connection.connect((err)=> {
        if(!err){
            console.log('Connection Established Successfully');
            //connection.end();
        }else{
            console.log('Connection Failed!'+ JSON.stringify(err,undefined,2));
        }
    });

```

### Tercera parte: Consulta simple

```javascript
    
    let query = 'SELECT * from tabla1';
    connection.query(query, (err, rows) => {
        if(err) throw err;
        console.log('Datos de tabla1: \n', rows);
        //connection.end();
    });
    
```

### Cuarta parte: Inserción con parámetros: 

```javascript
    
    let insertQuery = 'INSERT INTO ?? (??) VALUES (?)';
    let query2 = mysql.format(insertQuery,["tabla1","campoTexto","Añadido desde Node"]);
    
    connection.query(query2, (err, response) => {
        if(err) throw err;
        console.log(response.insertId);
        //connection.end();
    }); 
    
```

### Quinta parte: Búsqueda con parámetros:

```javascript
    
    let selectQuery = 'SELECT * FROM ?? WHERE ?? = ?';    
    let query3 = mysql.format(selectQuery,["tabla1","campoTexto", "Añadido desde Node"]);
    connection.query(query3, (err, data) => {
        if(err) throw err;
        console.log(data);
        //connection.end();
    }); 

    
```

### Sexta parte: Actualización con parámetros: 

```javascript
    
    let updateQuery = "UPDATE ?? SET ?? = ? WHERE ?? = ?";
    let query4 = mysql.format(updateQuery,["tabla1","campoTexto","Cambiado desde Node 2","id",1]);

    connection.query(query4, (err, response) => {
        if(err) throw err;
        console.log(response);
        console.log(query4);
        //connection.end();
    });

    
```

### Séptima parte: Borrado con parámetros: 

```javascript
    
    let deleteQuery = "DELETE from ?? where ?? = ?";
    let query5 = mysql.format(deleteQuery, ["tabla1", "id", 2]);

    connection.query(query5, (err, response) => {
        if(err) throw err;
        console.log(response);
        console.log(query5);
        //connection.end();
    });

    
```

### Octava parte: Llamada a procedimientos y funciones: 

```javascript 

    let pQuery = 'CALL ??';
    let pName ="todoTabla1"
    let query6 = mysql.format(pQuery,[pName]);
    connection.query(query6, (err, response) => {
        if(err) throw err;
        console.log(response);
        console.log(query6);
        //connection.end();

    });

    let query7 = 'SELECT primerID()';

    connection.query(query7, (err, response) => {
        if(err) throw err;
        console.log(response);
        console.log(query7);
        connection.end();
    });

```
