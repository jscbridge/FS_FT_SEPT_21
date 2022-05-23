![logotipo de The Bridge](https://user-images.githubusercontent.com/27650532/77754601-e8365180-702b-11ea-8bed-5bc14a43f869.png  "logotipo de The Bridge")
# [Bootcamp Web Developer Full Stack](https://www.thebridge.tech/bootcamps/bootcamp-fullstack-developer/)
### JS, ES6, Node.js, Frontend, Backend, Express, React, MERN, testing, DevOps
# BD Relacionales 2
## Introducción a SQL
Lenguaje diseñado y desarrollado para crear, administrar y gestionar Bases de Datos Relacionales.
Originalmente basado en álgebra relacional y cálculo relacional, se divide en tres partes diferenciadas: 
1.  Lenguaje de definición de datos (DDL)
2.  Lenguaje de manipulación de datos (DML)
3.  Lenguaje de control de datos (DCL)
4.  Lenguaje de control de transacciones (TCL)
El alcance de SQL incluye:
1.  Inserción, consulta, actualización y borrado de datos
2.  Creación, modificación y borrado de esquemas
3.  Control de datos
4.  Control de acciones sobre los datos y posibilidad de vuelta atrás 
- [Resumen](https://platzi.com/blog/que-es-ddl-dml-dcl-y-tcl-integridad-referencial/?utm_source=google&utm_medium=paid&utm_campaign=14603491644&utm_adgroup=&utm_content=&gclid=Cj0KCQjwtrSLBhCLARIsACh6RmiovgXc53IXWobhUoGKZmrMZVXmHCPQougHOpfBob0TMHQNc7R9dLoaAktnEALw_wcB&gclsrc=aw.ds)
## Creación de BD en base al diagrama ER
### Creación de BD en MySQL 
Lo que debemos indicar de forma obligatoria es su nombre. 
**Sintaxis:**
```
CREATE DATABASE nombreBD;
```
- [DOCUMENTACIÓN CREATE DATABASE](https://dev.mysql.com/doc/refman/8.0/en/create-database.html)
**Ejemplo básico:**
- CREATE DATABASE ejemplo;
### Borrado de BD en MySQL 
Lo que debemos indicar de forma obligatoria es su nombre.
**Sintaxis:**
```
DROP DATABASE nombreBD;
```
- [DOCUMENTACIÓN DROP DATABASE](https://dev.mysql.com/doc/refman/8.0/en/drop-database.html)
**Ejemplo básico:**
- DROP DATABASE ejemplo;
### Conexión de BD en MySQL 
Lo que debemos indicar de forma obligatoria es su nombre. 
**Sintaxis:**
```
USE nombreBD;
```
### Tipos de datos MySQL
Un tipo de dato define un dominio.
**Numéricos:**
| Tipo | Descripción | Valores que puede tomar |
| ------------ | ------------- | ------------- |
| BIT[LONGITUD] | BIT[LONGITUD] Un bit de información, si no especificamos longitud (que puede ser desde 1 a 64) toma por defecto 1    0 o 1 | 0 o 1 |
| BOOL, BOOLEAN |  Booleanos | Falso = 0 <br/> Verdadero = 1
| TINYINT | Entero corto | Sin signo = O a 255 <br/>Con signo =  -128 a 127 |
| SMALLINT | Entero corto |Sin signo = O a 65.535 <br/> Con signo =  -32.768 a 32.767 |
| MEDIUMINT | Entero medio |Sin signo = O a 16.777.215 <br/> Con signo =  -8.388.608 a 8.388.607
| INT, INTEGER | Entero |Sin signo = O a 4.294.967.295 <br/> Con signo = -2.147.483.648 a 2.147.483.647 |
| BIGINT | Entero   largo | Sin signo = O a 18.446.744.073.709.551.615 <br/> Con signo = -9.223.372.036.854.775.808 a 9.223.372.036.854.775.807 |
| DECIMAL [(longitud, decimales)]   | Número decimal en coma flotante |Longitud de hasta 65 cifras y decimales hasta 30 |
| DEC [(longitud, decimales)] <br/>NUMERIC [(longitud, decimales)] <br/>FIXED [(longitud, decimales)]   | Igual que DECIMAL |Longitud de hasta 65 cifras y decimales hasta 30 |
| FLOAT [(longitud, decimales)] | Número decimal en coma flotante | De 3.402.823.466 x 1038 a<br/> 1.175494351 x 10-38 <br/> o <br/> De 1.175494351 x 10-38 a <br/>3.402823466 x 1038 |
| DOUBLE[(longitud, decimales)] | Número decimal en coma flotante  | De -1.7976931348623157 x 10308 <br/> a -2.2250738585072014 x 10-308 <br/> o <br/> De 2.2250738585072014 x 10-308 <br/> a 1.7976931348623157 x 10308 |
**Fechas y horas:**
| Tipo | Descripción | Valores que puede tomar |
| ------------ | ------------- | ------------- |
| DATE  | Fecha  | Varios formatos, uno de ellos: “YYYY-MM-DD” |
| DATETIME [presicion]  | Fecha y hora  | Formato “YYYY-MM-DD HH:MM:SS.SSSSSS”, precisión define el número de decimales de los segundos.|
| TIME [presicion]  |Hora   | formato “HH:MM:SS, precisión valores de S |
| YEAR[(2 o 4)] | Fecha | Año representado en 2 cifras o 4 cifras |
**Cadenas de caracteres:**
| Tipo | Descripción | Valores que puede tomar |
| ------------ | ------------- | ------------- |
| CHAR [longitud]   | Cadena de longitud fija, debe tener el número de caracteres que diga longitud |  Caracteres alfanuméricos |
| VARCHAR [longitud] | Cadena de longitud variable, debe tener como máximo el número de caracteres que diga longitud | Caracteres alfanuméricos |
| TEXT  | Texto de longitud variable | Hasta 65535 caracteres alfanuméricos |
- [DOCUMENTACIÓN TIPOS DE DATOS](https://dev.mysql.com/doc/refman/8.0/en/data-types.html)
## Creación de tablas en MySQL
La creación de tablas implica indicar el nombre de la tabla, basándonos en el nombre de la entidad o relación, cuáles son los campos de las tablas, basándonos en los atributos de nuestro diseño de la BD, el tipo de los mismos y las restricciones (clave primaria, clave foránea y otras que veremos).
**Sintaxis general :** 
```
CREATE TABLE nombre (
    campo1 tipo [restricciones],
    campo2 tipo [restricciones],
    ...
    campoN tipo [restricciones]
);
```
### Clave primaria:
La clave primaria debe ser un entero autoincrementable, para optimizar el tiempo de búsqueda.
**Sintaxis:**
```
id INT AUTO_INCREMENT
...
PRIMARY KEY(id)
```
**Ejemplo de una tabla con clave primaria solamente:**
```
CREATE TABLE nombre (
    id INT AUTO_INCREMENT,
    PRIMARY KEY(id)
);
```
### Clave foránea:
La clave foránea debe ser un entero ya que apunta a una clave primaria.
**Sintaxis:**
```
fk_id_tabla INT,
...
FOREIGN KEY(fk_id_tabla) REFERENCES tabla(id)
```
**Ejemplo de una tabla con clave primaria y clave foránea:**
```
CREATE TABLE nombre (
    id INT AUTO_INCREMENT,
    fk_id_tabla INT,
    PRIMARY KEY(id),
    FOREIGN KEY(fk_id_tabla) REFERENCES tabla(id)
);
```
### Ejemplo tabla Personas con id, nombre y apellidos: 
```
CREATE TABLE Personas (
    id INT AUTO_INCREMENT,
    nombre VARCHAR(100),
    apellidos VARCHAR(200),
    PRIMARY KEY(id)
);
```
- [DOCUMENTACIÓN CREATE TABLE](https://dev.mysql.com/doc/refman/8.0/en/create-table-generated-columns.html)
## Restricciones
### NOT NULL
Restricción usada para indicar que el campo no se puede dejar vacío, debe tener un contenido.
**Ejemplos:**
- dni CHAR(9) NOT NULL
- email VARCHAR(20) NOT NULL
### UNIQUE
Restricción usada para indicar que el contenido del campo no se puede repetir.
**Ejemplos:**
- dni CHAR(9) UNIQUE 
- email VARCHAR(20) UNIQUE
### CHECK: Validación de campos
Para realizar comprobaciones sencillas del contenido de un campo podemos usar CHECK, esta validación se hace a nivel de BD y no hace falta capa de programación.
**Sintaxis:**
```
CHECK(expresion)
````
- La expresión es una condición que permite validar el campo.
**Ejemplos:**
- edad INT CHECK(edad >= 18) 
- email VARCHAR(20) UNIQUE
### ON UPDATE/ON DELETE 
Cuando tenemos una clave foránea, necesitamos gestionar lo que sucede cuando se actualiza o borra un campo al que apunta dicha clave foránea.
**Ejemplo:**
Imaginemos que tenemos una clave foránea al cliente con id 2 en la tabla compras, ¿qué sucede con la compra si borro al cliente con id 2?. Las opciones son varias: 
- RESTRICT/NO ACTION: Modo por defecto de las claves foráneas, indca que si el cliente con id 2 se encuentra referenciado en alguna compra, no se puede cambiar su id, ni se puede borrar.
- SET NULL: Indica que si actualizamos o borramos el cliente con id 2, se pondrá a NULL su referencia en las compras.
- CASCADE: ndica que si actualizamos o borramos el cliente con id 2, se se actualizarán o borrarán las compras de dicho cliente.
**Sintaxis:**
```
CREATE TABLE nombre (
    id INT AUTO_INCREMENT,
    fk_id_tabla INT,
    PRIMARY KEY(id),
    FOREIGN KEY(fk_id_tabla) REFERENCES tabla(id) ON DELETE opcion
);
```