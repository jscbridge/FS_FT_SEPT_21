![logotipo de The Bridge](https://user-images.githubusercontent.com/27650532/77754601-e8365180-702b-11ea-8bed-5bc14a43f869.png  "logotipo de The Bridge")


# [Bootcamp Web Developer Full Stack](https://www.thebridge.tech/bootcamps/bootcamp-fullstack-developer/)
### JS, ES6, Node.js, Frontend, Backend, Express, React, MERN, testing, DevOps

# BD Relacionales 4

## Acciones sobre los datos
La acciones que podemos hacer con los datos de una tabla son 4:

1.	Inserciones
2.	Actualizaciones
3.	Borrados
4.  Consultas o búsquedas

### Inserción

**Sintaxis básica:**
```
INSERT INTO tabla VALUES(valor1, valor2...valorN)
```
**Ejemplo:**
```
INSERT INTO clientes VALUES(NULL, 'Pedro Pérez'...);
```
- Los datos numéricos van sin comillas y las cadenas y fechas/horas con comillas.
- Se pueden usar dobles o simples
- El primer valor a NULL se usa para la PK, al llevar la cuenta la BD de los ids, lo ponemos a NULL y la BD le asigna su valor correspondiente.


- [DOCUMENTACIÓN INSERT](https://dev.mysql.com/doc/refman/8.0/en/insert.html)

### Actualización
**Sintaxis básica:**
```
UPDATE tabla SET campo = valor, campo2 = valor2, ..., campoN = valorN [WHERE condicion]
```

La actualización de datos se hace por campos, por ejemplo, podemos cambiar el apellido de un cliente
**Ejemplo:**
```
UPDATE clientes SET apellido1 = 'Ramírez' WHERE id = 8;
```
- Ojo: Si hacemos un UPDATE sin WHERE modificamos la columna en toda la tabla

- [DOCUMENTACIÓN UPDATE](https://dev.mysql.com/doc/refman/8.0/en/update.html)

### Borrado
Hay dos formas de borrar el contenido de una tabla: 

- DELETE 
- TRUNCATE

**Sintaxis básica DELETE:**
```
DELETE FROM tabla [WHERE condicion]
```

- Ojo: Si hacemos un DELETE sin WHERE vaciamos la tabla

**Ejemplo DELETE:**
```
DELETE FROM proveedores WHERE id = 7;
```

- [DOCUMENTACIÓN DELETE](https://dev.mysql.com/doc/refman/8.0/en/delete.html)

### Truncate: 
Permite vaciar la tabla y la resetea al estado inicial (justo después de crearla)
- Pone a 0 el contador del AUTO_INCREMENT
- Elimina toda la programación asociada a la tabla

**Sintaxis básica TRUNCATE:**
```
TRUNCATE TABLE tabla;
```

**Ejemplo TRUNCATE:**
```
TRUNCATE TABLE Clientes;
```

- [DOCUMENTACIÓN TRUNCATE](https://dev.mysql.com/doc/refman/8.0/en/truncate-table.html)

### Búsquedas
**Sintaxis básica:**
```
SELECT campo/s FROM tabla/s [WHERE condicion]
```


**Ejemplo:**
```
SELECT nombre FROM Clientes WHERE id > 10;
```


- [DOCUMENTACIÓN SELECT](https://dev.mysql.com/doc/refman/8.0/en/select.html)



### Ejercicios: 
1. Realiza dos inserts en las tablas de la BD del ejercicio del ejercicio del Instituto.
2. Actualiza la ciudad de los clientes con id 1 y 3 de la BD del ejercicio del Taller a Madrid
3. Borra los alumnos llamados Pedro en la BD del Instituto.
4. Muestra toda la información de todas las tablas de la BD del ejercicio del Taller.
5. Muestra el salario y la dirección de los camioneros de la BD del ejercicio de la Empresa de Transporte.




