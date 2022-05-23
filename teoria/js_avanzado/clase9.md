![logotipo de The Bridge](https://user-images.githubusercontent.com/27650532/77754601-e8365180-702b-11ea-8bed-5bc14a43f869.png  "logotipo de The Bridge")


# [Bootcamp Web Developer Full Stack](https://www.thebridge.tech/bootcamps/bootcamp-fullstack-developer/)
### JS, ES6, Node.js, Frontend, Backend, Express, React, MERN, testing, DevOps

## Clase 9

### API HTML5: Geolocalización

![Leaflet](../../assets/js_avanzado/clase9/geolocation.png)

La API de geolocalización permite al usuario compartir su ubicación a las aplicaciones web si así lo desea. Por razones de privacidad, al usuario se le pide que confirme el permiso para proporcionar información de ubicación.

- [MDN | Using Geolocation](https://developer.mozilla.org/es/docs/WebAPI/Using_geolocation)
- [Demo - geolocation](https://www.w3schools.com/html/html5_geolocation.asp)


Obtener ubicación actual

```javascript
if ("geolocation" in navigator) {
    navigator.geolocation.getCurrentPosition(position => {
         console.log(`Latitud: ${position.coords.latitude}\nLongitud: ${position.coords.longitude}`);
        let datos = `<h1>Aquí estás!</h1>
        <p>Lat: ${position.coords.latitude.toFixed(4)}</p>
        <p>Long: ${position.coords.longitude.toFixed(4)}</p>`
        document.body.innerHTML = datos;
    });
} else {
  console.warn("Tu navegador no soporta Geolocalización!! ");
}
```

Seguir a un usuario :grimacing:

```javascript
navigator.geolocation.watchPosition(position => {
     console.log(`${position.coords.latitude}, ${position.coords.longitude}`)
}, error => {
    console.warn(`Error! - ${error}`);
});
```


### Leaflet
Vamos a probar una librería Open Source para dibujar mapas.
- [Leaflet](https://leafletjs.com/)

![Leaflet](../../assets/js_avanzado/clase9/leaflet.png)

### Instrucciones para usar Leaflet :unicorn:
Entre todas las herramientas y librerias que tenemos en el frontend para pintar mapas, **Leaflet** es una librería Open Source que permite integrar gestores de mapas en sus funciones de pintado, convirtiéndola en una librería ideal para aprender a trabajar con mapas y conseguir excelentes resultados en nuestros proyectos.
**Pasos para integrar Leaflet**
1. Añadir link al CSS de Leaflet en `<head></head>` y script al final del `<body></body>`:
```html
<!-- Link Leaflet CSS -->
<link
  rel="stylesheet"
  href="https://unpkg.com/leaflet@1.7.1/dist/leaflet.css"
  integrity="sha512-xodZBNTC5n17Xt2atTPuE1HxjVMSvLVW9ocqUKLsCC5CXdbqCmblAshOMAS6/keqq/sMZMZ19scR4PsZChSR7A=="
  crossorigin=""
/>
<!-- Script Leaflet JS -->
<script
  src="https://unpkg.com/leaflet@1.7.1/dist/leaflet.js"
  integrity="sha512-XQoYMqMTK8LvdxXYG3nZ448hOEQiglfqkJs1NOQV44cWnUrBc8PkAOcXy20w0vlaXaVUearIOBhiXZ5V3ynxwA=="
  crossorigin=""
></script>
```
2. Crea un `div` que contenga un `id` única en el que inyectaremos el mapa:
```html
<div id="map"></div>
```
3. Dale estilos al `div` para que podamos verlo sin problemas en el navegador:
```css
#map {
  height: 400px;
  width: 350px;
  border: 1px solid black;
}
```
4. Inyecta el mapa usando **Leaflet** a través del script que habíamos importado. Para ello crea un archivo `index.js` (o con el nombre que prefieras) y utiliza este código:
```javascript
const mapId = 'map';
const initialCoordinates = [40.4169473, -3.7057172]; // Plaza Sol en Madrid [lat, lng]
const map = L.map(mapId).setView(initialCoordinates, 13);
```
- Ahora verás que el mapa creado es gris y no somos capaces de ver su contenido. Esto se debe a que necesitamos usar una librería de `tiles`, es decir, las piezas que conforman el mapa tal y como lo conocemos.
5. Como librería de `tiles` a añadir, utilizaremos **Mapbox**.
- Crearemos para esto un string al que interpolaremos variables a través de una función de **Leaflet**:
```javascript
const MAPBOX_API = 'https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token={accessToken}'
```
- Ahora iremos a la web de **Mapbox** y nos registraremos para obtener una API key y añadiremos las siguientes variables:

```javascript
const ATTRIBUTION =
  'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, <a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, Imagery © <a href="https://www.mapbox.com/">Mapbox</a>';
// Este token será el que obtengamos en la web de Mapbox
const ACCESS_TOKEN =
  'pk.eyJ1IjoiY2Nhc3RpbGxvMDZtYiIsImEiOiJja2k1eXpybXU3em1mMnRsNjNqajJ0YW12In0.aFQJlFDBDQeUpLHT4EiRYg';
```
- Por último, lanzaremos la siguiente función de **Leaflet** para cargar todos los tiles de **Mapbox** en nuestro mapa:

```javascript
L.tileLayer(MAPBOX_API, {
  attribution: ATTRIBUTION,
  maxZoom: 18,
  id: 'mapbox/streets-v11',
  tileSize: 512,
  zoomOffset: -1,
  accessToken: ACCESS_TOKEN
}).addTo(map);
```

6. Ahora que vemos el mapa correctamente, vamos a añadir un marcador (a lo Google!) para que los usuarios de nuestra web puedan apreciar donde se encuentra el punto que hemos centrado. Para ello, usaremos las coordenadas iniciales (aunque ahora puedes poner tantas como quieras en distintos sitios) e invocaremos a una nueva función de \*+Leaflet\*\*:

```javascript
// Añadimos el marcador a nuestra posición inicial
L.marker(initialCoordinates).addTo(map);
 // Ejemplo añadiendo otras coordenadas:
const plazaMayorCoordinates = [40.4168898,-3.7020553]
L.marker(plazaMayorCoordinates).addTo(map);
```
7. Para terminar con nuestro mapa, añadiremos un popup sobre los marcadores que tenemos para resaltar información sobre ellos. Modifica el código del paso anterior y añade `.bindPopup(...)` a cada marker de la siguiente forma:

```javascript
// Añadimos el marcador a nuestra posición inicial
L.marker(initialCoordinates).bindPopup("<b>Plaza Sol</b><br>Posición inicial del mapa").addTo(map);
// Ejemplo añadiendo otras coordenadas:
const plazaMayorCoordinates = [40.415511, -3.7095896];
L.marker(plazaMayorCoordinates).bindPopup("<b>Plaza Mayor</b><br>Posición adicional").addTo(map);
```


### Ejercicios
#### 1. Utiliza Leaflet para posicionarte en un mapa

#### 2. Posicionar el transporte público (trenes y autobuses) de Los Angeles en el mapa. :tada: :bus: :tram:

Tendrás que hacer:
- Fetch de la posición de los vehículos en tiempo real
- Después de hacer fetch(), tratar el objeto para poder pintar los puntos con Leafelt

#### Avanzado: 
- Haz que se refresque la posición de los vehículos en el mapa cada 3 segundos para dar efecto de "movimiento"
- Con un popup, dibujar el ID del vehículo

Recursos:
- [API de Metro.net de LA](https://developer.metro.net/)
- [Mapbox - proveedor de mapas en línea](https://www.mapbox.com/)