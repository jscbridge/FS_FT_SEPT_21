![logotipo de The Bridge](https://user-images.githubusercontent.com/27650532/77754601-e8365180-702b-11ea-8bed-5bc14a43f869.png  "logotipo de The Bridge")


# [Bootcamp Web Developer Full Stack](https://www.thebridge.tech/bootcamps/bootcamp-fullstack-developer/)
### JS, ES6, Node.js, Frontend, Backend, Express, React, MERN, testing, DevOps

## Clase 7

### Gráficas 

![Chart](../../assets/js_avanzado/clase7/chart.jpeg)

**Librerías**
- [Chart.js](http://www.chartjs.org/)

![Chart.js](../../assets/js_avanzado/clase7/chartjs.jpg)

- [Chartist.js](http://gionkunz.github.io/chartist-js/)

![Leaflet](../../assets/js_avanzado/clase7/chartist.gif)

### Gráficas avanzadas - D3.js
>D3.js es una biblioteca de JavaScript para producir, a partir de datos, infogramas dinámicos e interactivos en navegadores web. Hace uso de tecnologías bien sustentadas como SVG, HTML5, y CSS [Wikipedia](https://es.wikipedia.org/wiki/D3.js)

![Chart.js](../../assets/js_avanzado/clase7/d3js.jpg)
- [D3.js](https://d3js.org/)
- [D3.js - Examples](https://observablehq.com/@d3/gallery)

- [Codepen | CSS 3D Solar System](https://codepen.io/juliangarnier/pen/idhuG)
- [Codepen | D3 canvas globe with country hover](https://codepen.io/jorin/pen/YNajXZ)
- [Codepen | Airport Distance Map](https://codepen.io/shshaw/pen/vJNMQY)

### Más librerías
- [amazing-graphical-javascript-frameworks](https://www.creativebloq.com/features/amazing-graphical-javascript-frameworks)
- [these-are-the-best-javascript-chart-libraries-for-2019]( https://www.freecodecamp.org/news/these-are-the-best-javascript-chart-libraries-for-2019-29782f5e1dc2/)
- [top-picks-javascript-chart-libraries](https://blog.logrocket.com/top-picks-javascript-chart-libraries/)
 -[best-javascript-data-visualization-libraries-for-2020](https://medium.com/javascript-in-plain-english/best-javascript-data-visualization-libraries-for-2020-15291919a176)



### Ejercicio

Practicaremos cómo crear gráficas con las librerías vistas en clase

1. Pediremos las películas de Star Wars y pintaremos una gráfica de líneas en la que podamos ver cada una de las películas.
- En el **eje X** el nombre de la película
- En el **eje Y** año de publicación

```
API ENDPOINT --> https://swapi.dev/api/films/
```

2. Pediremos los personajes de Star Wars y pintaremos una gráfica de barras en la que podamos ver
- En el **eje X** el nombre del personaje
- En el **eje Y** el número de películas en las que ha participado.

```
API ENDPOINT --> https://swapi.dev/api/people/
```

Para pintar todo esto usaremos `Chartist`
Link a la docu: [Chartist](https://gionkunz.github.io/chartist-js/api-documentation.html)

