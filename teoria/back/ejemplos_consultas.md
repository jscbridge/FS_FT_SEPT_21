![logotipo de The Bridge](https://user-images.githubusercontent.com/27650532/77754601-e8365180-702b-11ea-8bed-5bc14a43f869.png  "logotipo de The Bridge")


# [Bootcamp Web Developer Full Stack](https://www.thebridge.tech/bootcamps/bootcamp-fullstack-developer/)
### JS, ES6, Node.js, Frontend, Backend, Express, React, MERN, testing, DevOps

**Código de ejemplos de consultas:**

```
#DROP DATABASE Hospital;
CREATE DATABASE Hospital;

USE Hospital;

CREATE TABLE Camas(
	id_cama INT AUTO_INCREMENT,
    zona VARCHAR(50), 
    planta VARCHAR(50) NOT NULL,
    fechaCambioSabanas DATE NOT NULL, 
    PRIMARY KEY(id_cama)
);

INSERT INTO Camas VALUES(null, "pediatría", "Primera", "2020/01/29");
INSERT INTO Camas VALUES(null, "cardiología", "Primera", "2020/01/30");
INSERT INTO Camas VALUES(null, "traumatología", "Segunda", "2020/02/15");
INSERT INTO Camas VALUES(null, "traumatología", "Segunda", "2021/02/16");
INSERT INTO Camas VALUES(null, "obstetricia", "Tercera", "2019/01/29");
INSERT INTO Camas VALUES(null, "ginecología", "Cuarta", "2020/01/29");

CREATE TABLE Pacientes(
	id_paciente INT AUTO_INCREMENT,
    nombre VARCHAR(100),
    apellido1 VARCHAR(100),
    dni CHAR(9) NOT NULL,
    fechaIngreso DATE,
    fk_id_cama INT,
    PRIMARY KEY(id_paciente)
);
INSERT INTO Pacientes VALUES(null, "María", "Pérez", "11111111A", "2020/01/28", 1);
INSERT INTO Pacientes VALUES(null, "María", "Pérez", "11111111A", "2020/02/14", 3);
INSERT INTO Pacientes VALUES(null, "María", "Pérez", "11111111A", "2020/02/29", 2);
INSERT INTO Pacientes VALUES(null, "José", "Ramirez", "22222222B", "2020/02/10", 3);
INSERT INTO Pacientes VALUES(null, "Rafael", "Hernández", "33333333C", "2020/01/09", 4);
INSERT INTO Pacientes VALUES(null, "Ana", "Rodríguez", "44444444D", "2020/01/26", 6);
INSERT INTO Pacientes VALUES(null, "Ana", "Rodríguez", "44444444D", "2020/01/27", 5);

CREATE TABLE Medicos(
	id_medico INT AUTO_INCREMENT,
    nombre VARCHAR(100),
    apellido1 VARCHAR(100),
    apellido2 VARCHAR(100),
    dni CHAR(9) UNIQUE NOT NULL,
    turno VARCHAR(50), 
	especialidad VARCHAR(100) NOT NULL, 
	PRIMARY KEY(id_medico) 
);
INSERT INTO Medicos VALUES(null, "Rosa", "Hernández", "Ruíz", "55555555A", "Mañana", "pediatría");
INSERT INTO Medicos VALUES(null, "Juan", "Ruíz", "Ruíz", "55555555B", "Tarde", "pediatría");
INSERT INTO Medicos VALUES(null, "Carlos", "Blanco", "Pérez", "55555555C", "Mañana", "cardiología");
INSERT INTO Medicos VALUES(null, "Carlos", "Hernández", "Pérez", "55555555D", "Tarde", "cardiología");
INSERT INTO Medicos VALUES(null, "Ana", "Ramirez", "Pérez", "55555555E", "Mañana", "traumatología");
INSERT INTO Medicos VALUES(null, "Gabriela", "Betancort", "Seoane", "55555555F", "Tarde", "traumatología");
INSERT INTO Medicos VALUES(null, "Juan", "Ramirez", "Seoane", "55555555G", "Mañana", "obstetricia");
INSERT INTO Medicos VALUES(null, "David", "Díaz", "Pérez", "55555555H", "Tarde", "obstetricia");
INSERT INTO Medicos VALUES(null, "Gabriela", "Martínez", "Seoane", "55555555I", "Mañana", "ginecología");
INSERT INTO Medicos VALUES(null, "Óscar", "Martínez", "Pérez", "55555555J", "Tarde", "ginecología");


CREATE TABLE Pacientes_Medicos(
	id_paciente_medico INT AUTO_INCREMENT,
    fk_id_paciente INT,
    fk_id_medico INT, 
    PRIMARY KEY(id_paciente_medico)
);

INSERT INTO Pacientes_Medicos VALUES(null, 1, 1);
INSERT INTO Pacientes_Medicos VALUES(null, 1, 2);
INSERT INTO Pacientes_Medicos VALUES(null, 2, 3);
INSERT INTO Pacientes_Medicos VALUES(null, 3, 5);
INSERT INTO Pacientes_Medicos VALUES(null, 4, 6);
INSERT INTO Pacientes_Medicos VALUES(null, 5, 6);
INSERT INTO Pacientes_Medicos VALUES(null, 5, 5);
INSERT INTO Pacientes_Medicos VALUES(null, 6, 9);
INSERT INTO Pacientes_Medicos VALUES(null, 6, 10);
INSERT INTO Pacientes_Medicos VALUES(null, 7, 7);
INSERT INTO Pacientes_Medicos VALUES(null, 7, 8);

ALTER TABLE Pacientes
ADD FOREIGN KEY (fk_id_cama) REFERENCES Camas (id_cama) ON UPDATE CASCADE ON DELETE SET NULL;

ALTER TABLE Pacientes_Medicos
ADD FOREIGN KEY (fk_id_paciente) REFERENCES Pacientes (id_paciente) ON UPDATE CASCADE ON DELETE SET NULL,
ADD FOREIGN KEY (fk_id_medico) REFERENCES Medicos (id_medico) ON UPDATE CASCADE ON DELETE SET NULL;

# Obtener el apellido de todos los pacientes no llamados María

SELECT nombre 
FROM Pacientes
WHERE nombre<>"María";

# Obtenerla zona y planta de las camas a las que no se les ha cambiado sábanas el 16 de febrero de 2021

SELECT zona,planta
FROM Camas
WHERE NOT (fechaCambioSabanas="2021-02-16");

# Obtener el id_paciente del paciente con DNI 33333333C (ids de pacientes que no sean 33333333C)

SELECT id_paciente
FROM Pacientes
WHERE dni<>"33333333C";

# Obtener turno, nombre y especialidad de los médicos con id_medico diferentes de 2, 4 y 5

SELECT turno,nombre,especialidad
FROM Medicos
WHERE id_medico<>2 AND id_medico<>4 AND id_medico<>5;


# Medicos con especialidad que no sea cardiología

SELECT *
FROM Medicos
WHERE especialidad<>"Cardiología";

# id Médicos que no han atendido al paciente 2

SELECT fk_id_medico
FROM Pacientes_Medicos
WHERE fk_id_paciente<>2;

# ids médicos no han atendido a ningún paciente 

SELECT id_medico
FROM Medicos
WHERE id_medico NOT IN (SELECT fk_id_medico FROM Pacientes_Medicos);

# Pacientes atendidos x médicos que no sean los de id 7 y 9

SELECT fk_id_paciente
FROM Pacientes_Medicos
WHERE fk_id_medico<>7 AND fk_id_medico<>9;
# WHERE NOT (fk_id_medico=7 OR fk_id_medico=9);


# Eliminar duplicados sobre ejercicio ids médicos han atendido algún paciente 

SELECT DISTINCT (fk_id_medico)
FROM Pacientes_Medicos;

SELECT SUM(id_medico)
FROM Medicos;

SELECT COUNT(*) AS CUANTAS_MARIAS
FROM Pacientes
WHERE nombre="María";

SELECT AVG(id_medico)
FROM Medicos;

# Nombre de todos los médicos que han atendido pacientes OK;

SELECT nombre
FROM Medicos
WHERE id_medico IN (SELECT fk_id_medico FROM Pacientes_Medicos);

# Zona de las camas en las que han estado pacientes OK:

SELECT DISTINCT(zona)
FROM Camas
WHERE id_cama IN (SELECT fk_id_cama FROM Pacientes);

# Nombre del médico y nombre del paciente en cada atención OK;

SELECT Medicos.nombre,Pacientes.nombre
FROM Medicos,Pacientes
WHERE (id_medico, id_paciente) IN (SELECT fk_id_medico, fk_id_paciente FROM Pacientes_Medicos);

# DNI y especialidad de los médicos que han atendido a pacientes que se apellidan Pérez OK,

SELECT dni,especialidad
FROM Medicos
WHERE id_medico IN (SELECT fk_id_medico 
					FROM Pacientes_Medicos 
                    WHERE fk_id_paciente IN 
						(SELECT id_paciente 
						FROM Pacientes 
						WHERE apellido1="Pérez"));
                        
# Pacientes atendidos por médicos de pediatría OK;

SELECT *
FROM Pacientes
WHERE id_paciente IN(SELECT fk_id_paciente 
					FROM Pacientes_Medicos 
                    WHERE fk_id_medico IN
						(SELECT id_medico
                        FROM Medicos
                        WHERE especialidad="pediatría"));
                        
# Obtener la cantidad de veces que aparece el paciente con id 1 en la tabla Pacientes;

SELECT COUNT(id_paciente)
FROM Pacientes
WHERE id_paciente=1;

# Obtener la suma los ids de los médicos que se llaman Carlos;

SELECT SUM(id_medico)
FROM Medicos
WHERE nombre="Carlos";

# Obtener los apellidos que hay en la tabla Pacientes sin repetir;

SELECT DISTINCT apellido1
FROM Pacientes;

# Obtener la suma, cantidad y media de los ids de las camas;

SELECT SUM(id_cama),COUNT(id_cama),AVG(id_cama)
FROM Camas;

# Obtener los médicos que no han atendido a la paciente María Pérez, ni a Ana Rodríguez;

SELECT *
FROM Medicos
WHERE id_medico IN(SELECT fk_id_medico FROM Pacientes_Medicos WHERE fk_id_paciente IN 
						(SELECT id_paciente FROM Pacientes WHERE (nombre<>"María" AND apellido1<>"Pérez") OR (nombre<>"Ana" AND apellido1<>"Rodríguez")));
                        
                        
SELECT * FROM pACIENTES;
SELECT * FROM Pacientes_medicos;


SELECT id_medico
FROM Medicos
WHERE id_medico IN(SELECT fk_id_medico FROM Pacientes_Medicos WHERE fk_id_paciente IN 
						(SELECT id_paciente FROM Pacientes WHERE nombre<>"Ana" AND apellido1<>"Rodríguez"));
                        
# Actualizar el nombre y apellido de los pacientes atendidos por Gabriela Martínez Seoane a Marta Ramírez OK;

UPDATE Pacientes
SET nombre="Marta", apellido1="Ramírez"
WHERE id_paciente IN (SELECT fk_id_paciente FROM Pacientes_Medicos WHERE fk_id_medico IN
						(SELECT  id_medico FROM Medicos WHERE nombre="Gabriela" AND apellido1="Martínez" AND apellido2="Seoane"));  
                        
SELECT *
FROM Pacientes;                        
```
