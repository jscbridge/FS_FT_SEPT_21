# Ejercicio de navidad - NasaAPP

![img](../../assets/react/ejercicioNavidad/merry-christmas-nasa.gif)

​
En este proyecto aplicaremos todo lo aprendido hasta ahora.  
​
El proyecto constará de dos partes: 
- **Parte visual de la aplicación**: debe ser responsive, mobile-first. Usaremos `React` funcional para diseñar el front

- **Parte de la API**
​
## NOTA IMPORTANTE
Para poder hacer la parte WEB debe hacerse en primer lugar la parte de la API, ya que necesitaréis los endpoints de la API.

## Requisitos
Para ello, debes tener en cuenta las siguientes consideraciones, que serán imprescindibles para este proyecto: 
​
- Respetar los principios y técnicas de lo que hemos aprendido durante el curso sobre HTML5, CSS3/SASS, ES6
- Frontend: Utilizar react FUNCIONAL.
- JS: manipulación del DOM, asincronía, promesas, fetch/axios, async/await... Utilizar el lenguaje JS con los principios utilizados en clase. 
- Se permite el uso de cualquier `recurso de terceros` (librerías, paquetes npm, etc.) que nos pueda facilitar el desarrollo.
- Gestión del `control de versiones con GiHub` desde el principio del proyecto. Rama main, develop y ramas feature correspondientes.
- Se prestará especial atención a un código limpio, legible, bien documentado, correctamente versionado y fácil de mantener, así como a la aplicación sobre el mismo de los `principios SOLID`
​
​
 ## Respecto a la API 
 
Todas las rutas de la API deben empezar con localhost:3000/api/

​
El ejercicio constará de 2 colecciones totales (landings y neas)
​
​
### Colección Landings

- Ruta base: `http://localhost:3000/api/astronomy/landings`
​
  1. **GET** para obtener nombre y masa de todos aquellos meteoritos cuya masa sea igual o superior a una masa (gr) dada (con query parameters)
​
  - Ejemplo: `/astronomy/landings?minimum_mass=200000`
​
  2. **GET** para obtener nombre y masa de uno o más meteoritos cuya masa sea la especificada (route params)
​
  - Ejemplo: `/astronomy/landings/mass/200000`
​
  3. **GET** para obtener los nombres y clase de aquellos meteoritos cuya clase sea la registrada (route params)
​
  - Ejemplo: `/astronomy/landings/class/L6`
​
  4. **GET** para obtener nombre, masa y fecha de todos los meteoritos caídos en determinadas fechas de la siguiente manera:
​
  - `/astronomy/landings?from=1960&to=1990`
  - `/astronomy/landings?from=1960`
  - `/astronomy/landings?to=1990`
  - El mismo endpoint deberá ser compatible con las 3 formas
​
### Colección NEAs

- Ruta base: `http://localhost:3000/api/astronomy/neas`
​
  1. **GET** para obtener la designación y el período anual en base a la clase orbital del asteroide (con query params)
​
  - Ejemplo: `/astronomy/neas?class=aten`
​
  2. **GET** para obtener designación, fecha y período anual de todos los asteroides que cumplan el filtro de fechas dadas
​
  - `/astronomy/neas?from=2010&to=2015`
  - `/astronomy/neas?from=2010`
  - `/astronomy/neas?to=2015`
  - En este caso, además, podremos poner la fecha más específica si quisiéramos:
    - `YYYY-MM-DD`
    - `YYYY-MM`
    - `YYYY`
  - El endpoint debe ser compatible con los 3 casos
​​

 ![img](../../assets/react/ejercicioNavidad/nasa.jpg)

 ## Respecto a la parte WEB

**Home:**

`GET http://localhost:3000/`
​

En la vista home aparecerán:
- Usar la [API de la NASA](https://api.nasa.gov/) para obtener la APOD(Astronomy Picture Of the Day) y dibujarla en el front. 
- Barra de navegación: Home, Asteroides, NEAs

**Sobre Landings:** 

`GET http://localhost:3000/landing`
-  Pintar en un mapa con Leaflet las localizaciones de los asteroides.
- Añadir algún filtro para seleccionar lo que quiero visualizar en el mapa. Ejemplo: 
  - Input + botón de filtro por peso
  - Input + botón de filtro por clase
  - Select para filtrar algún campo
- Pintar en el mapa labels con los detalles del meteorito   
```javascript
[
  {
    "name": "Aachen",
    "id": "1",
    "nametype": "Valid",
    "recclass": "L5",
    "mass": "21",
    "fall": "Fell",
    "year": "1880-01-01T00:00:00.000",
    "reclat": "50.775000",
    "reclong": "6.083330",
    "geolocation": { "latitude": "50.775", "longitude": "6.08333" }
  },
  ...
]
``` 

**Sobre NEAs**

`GET http://localhost:3000/neas`
- Pintar en unas tarjetas el detalle de cada NEA con los datos traídos de nuestra API creada anteriormente

```javascript
[
  {
    "designation": "419880 (2011 AH37)",
    "discovery_date": "2011-01-07T00:00:00.000",
    "h_mag": "19.7",
    "moid_au": "0.035",
    "q_au_1": "0.84",
    "q_au_2": "4.26",
    "period_yr": "4.06",
    "i_deg": "9.65",
    "pha": "Y",
    "orbit_class": "Apollo"
  },
  ...
]
```

​​
## Importación de datos en MongoDB

- [Datos ejercicio](../../utils/ejercicioNavidad)


**OPCIÓN 1 (la fácil)**:

En MongoCompass, creamos una colección. En dicha colección aparece el botón `add data`. Al pulsar en el botón aparecerá la opción de `Import File`. Pulsada esta opción nos aparecerá un cuadro de texto que nos permite seleccionar el archivo JSON que queremos importar en nuestra colección.

El ejercicio consta de dos colecciones que tenemos que importar. 

Los JSON de datos que queremos guardar te los adjuntamos en este ejercicio, en la carpeta utils. 

**OPCIÓN 2**:

El seeding nos permite importar grandes cantidades de datos a colecciones vacías. En este caso de adjuntamos la carpeta utils con dos JSON, uno referente a landings y otro referente a la colección neas. Para poder guardarlos dentro de nuestra base de datos de mongo, usaremos `mongoimport`.

```
mongoimport
```
1. Comprobar si tenemos instalado mongoimport

```
mongoimport --version
```
2. [Instalación de mongoimport]('https://docs.mongodb.com/database-tools/installation/installation/') (MongoDB Database Tools)

***

#### Uso
El comando neccesita que especifiquemos la __base de datos__, la __colección__, y la __ruta al archivo__ (csv y json)

```
mongoimport --db=[base-de-datos] --collection=[colección] [ruta/al/archivo]
```
Si usamos un json que se compone de un array de objetos deberemos pasar también un flag que lo especifique

```
mongoimport --jsonArray --db=[base-de-datos] --collection=[colección] [ruta/al/archivo]
```
***