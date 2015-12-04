# Introducción practica a D3.js 

Para trabajar con D3 es necesario tener conocimientos de HTML, CSS y JavaScript.

D3 utiliza el marcado SVG. SVG es un formato que utiliza texto para desplegar imágenes, osea una imagen SVG puede ser definida utilizando código de etiquetas al igual que HTML.


Practica rapida, vamos primero a dibujar con SVG, algo básico, un circulito.

```html
<svg width="100" height="100">
    <circle cx="50" cy="50" r="25"
    fill="blue" stroke="gray" stroke-width="2"/>
</svg>
```

Al tag “svg” le damos un alto y un ancho de 100px que es donde vamos a dibujar, dentro del mismo con el tag <circle> le damos la posición de 25px en el eje X y la posición al 25px del eje Y, este tag permite el radio del círculo que lo pusimos en 25px.

Fácil?, en resumen armamos un “campo” donde dibujar y centramos según el eje X e Y y le dimos el tamaño al círculo “seteando” su radio.

[Demo SVG][svg-example]

Bien ahora vamos a construir nuestro primer despliegue de datos con D3, lo primero obvio es descargar la librería o usar un CDN, llamar la librería en el documento HTML y esas cosas que se hacen al crear un nuevo proyecto :)

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="utf-8">
        <title>D3 Front End MELI</title>
        <script src="https://cdnjs.cloudflare.com/ajax/libs/d3/3.5.10/d3.min.js"></script>
    </head>
    <body>
        <script>
        //Codigo D3 por aca!
        </script>
    </body>
</html>
```

Primero vamos a utilizar la libreria D3 para añadir un elemento.  
En el mismo código de ejemplo agregamos la linea

```js
d3.select(“body”).append(“p”).text("¡Hola Frontenders!");
```

Aquí lo que hacemos es utilizar la referencia al objeto D3, que contiene el método select() que nos permite seleccionar el tag body y pasarle al (similar al encadenamiento de métodos de jQuery) método text() que escribirá el texto "¡Hola Frontenders!"

El codigo quedaria asi:

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="utf-8">
        <title>D3 Front End MELI</title>
        <script src="https://cdnjs.cloudflare.com/ajax/libs/d3/3.5.10/d3.min.js"></script>
    </head>
    <body>
        <script>
        d3.select(“body”).append(“p”).text(“¡Hola Frontenders!”);
        </script>
    </body>
</html>
```

Bien, ahora un poco mas complejo, vamos a representar los siguientes datos.

Tenemos la siguiente cadena:

```js
var datas = [ 8, 16, 32, 40, 60, 50, 20];
```

A esta cadena la vamos a manipular con D3 para plasmar los datos de la cadena.

```js
d3.select('body').selectAll('p')
    .data(datas)
    .enter()
    .append('p')
    .text(function(d) {
        return d;
    });
```

Aquí lo que hacemos primero es seleccionar “body” y con selectAll() para seleccionamos todos los “p” que se van a crear, en el cual cada “p” tendrá cada dato del array, esto se guarda temporalmente con el método enter() y lo aplica al añadir finalmente los “p” con append()

Al final como este código se ejecuta 7 veces (el array datas) a cada <p> le agrega el texto de su correspondiente número (8, 16, 32, 40, 60, 50, 20)

Resultado:
[Demo D3 con <P>][D3-P-example]


Ahora vamos a crear un simple gráfico de barras con D3

Utilizando el mismo array:
```js
var datas = [ 8, 16, 32, 40, 60, 50, 20];
```

Al código vamos a seleccionar el body y a crear un área para dibujar:

```js
d3.select("body").selectAll("div")
    .data(datas)
    .enter()
    .append("div")
    .attr("class", "bar");
```

Primero utilizamos el método selectAll() para indicarle a D3 que vamos a seleccionar todos los futuros <div> y que los guarde temporalmente, luego con el método datas() contamos la cantidad de elementos del array datas[] y le decimos con enter() las veces que debe ejecutarlo, hasta llegar a append() cuando los añadimos.

Ahora vamos a darle a cada barra su tamaño dependiendo el valor del elemento del array que le corresponda.

```js
d3.select('body').selectAll('div')
    .data(datas)
    .enter()
    .append('div')
    .attr('class', 'bar')
    .style('height', function(d) {
        var barHeight = d;
        return barHeight + 'px';
    });
```

Aquí lo que hicimos fue agregar el método attr() para darle la clase CSS a utilizar y con el método style() modificaremos de forma inline el alto según el dato del elemento del array que le corresponda a esa barra.

Resultado: [Demo][D3-DIV-example]

#Practica

Forkeamos desde jsfiddle para comenzar la practica:  
https://jsfiddle.net/rorjnq6f/

Paso a paso con cada resultado:  
Agregamos el metodo selectAll() a todos los rect  
https://jsfiddle.net/v617mrat/

Le damos el alto y ancho correspondiente y acorde  
https://jsfiddle.net/chdkunco/

Movemos por el eje X los gráficos así son legibles.  
https://jsfiddle.net/e45md5mo/

Invertimos el grafico SVG para ser legible en el alto  
https://jsfiddle.net/hxqwtxL9/

Agregamos fill para colorearlo y listo!  
https://jsfiddle.net/peo47xrk/


   [svg-example]: <https://jsfiddle.net/uum8venr/>
   [D3-P-example]: <https://jsfiddle.net/3dah3Lc3/>
   [D3-DIV-example]: <https://jsfiddle.net/y7zs2bzk/>
