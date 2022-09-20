## 💃 AdaLoversConf22-WIP

En este tutorial veremos conceptos básico de HTML, CSS y JS. Tocaremos transiciones, data-attributes, flexbox... no hace falta ser una experta para seguir este tutorial, si sabéis que estos lenguajes web existen, es todo lo que se necesita 🤘

### 🏗 Arquitectura de archivos

Estos son los archivos necesarios para nuestro proyecto:

1. Creamos la carpeta de `memory-game`
2. Entramos en la carpeta creada
3. Dentro generamos los archivos `index.html` `styles.css` `scripts.js`
4. Creamos la carpeta `assets` 

En la consola:
- 🎸  mkdir memory-game
- 🎸  cd memory-game
- 🎸  touch index.html styles.css scripts.js
- 🎸  mkdir assets

### 🍱 Cositas en nuestro HTML
En el archivo `index.html` tenemos que linkar los dos archivos que hemos creado, el `styles.css` y el `scripts.js`.

```
<!-- index.html -->
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">

  <title>Super Mario Bros 3 - Juego de memoria</title>

  <link rel="stylesheet" href="./styles.css">
</head>
<body>
  <script src="./scripts.js"></script>
</body>
</html>
```

### 🃏 Nuestro jueguico de cartas
El juego tiene 18 cartas, cada una está creada por un `div` contenedor que hemos llamado `.memory-card`, el cuál tiene dos imágenes `SVG`. La primera imágen será la cara frontal `front-card` y la segunda será común a todas, con el logo original de Nintendo cómo `back-card`.

```
<div class="memory-card">
  <img
    class="front-card"
    src="assets/svg/flower-snow.svg"
    alt="Flor de Nieve"
  />
  <img
    class="back-card"
    src="assets/svg/nintendo.svg"
    alt="Logo de Nintendo"
  />
</div>
```
### 🍱 Layout principal

![Board back](https://assets.codepen.io/527512/board-back.png)
![Board front](https://assets.codepen.io/527512/board-front.png)

```
<section class="memory-game"></section>
```

### 🍍 Dando estilo a nuestro jueguico

Utilizaremos un reset muy básico pero efectivo 👇

```
/* reset.css */

* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
```

Un poco de teoría:

- El modelo de caja 'box-sizing': La propiedad `border-box` incluye los padding y valores de borders dentro del tamaño total del elemento, width y height. Así simplificamos los cálculos.

// TODO
- Indicando al body que tenga un `display: flex` y un `margin: auto` a la clase .memory-game que actua como contenedo, creamo una alineación vertical y horaizontal.

- La clase `.memory-game` también será un contenedor con comportamiento `flex-container`. Por defecto, los elementos vienen seteados con `shrink` en lo ancho para ajustarse al contenedor. Seteando `flex-wrap` con el valor `wrap`, los `flex-items` se wrapearan a lo largo de multiples lineas dependiendo de su propio tamaño.

```
/* styles.css */

body {
  height: 100vh;
  display: flex;
  background: #060AB2;
}

.memory-game {
  width: 640px;
  height: 640px;
  margin: auto;
  display: flex;
  flex-wrap: wrap;
}
```
### 🍍 Dando estilo a nuestro jueguico
Each card width and height is calculated with calc() CSS function. Let’s make three rows, four card each by setting width to 25% and height to 33.333% minus 10px from margin.

In order to position .memory-card children, let’s add position: relative so we can position the children absolutely, relative to it.

The property position: absolute set to both front-face and back-face, will remove the elements from the original position, and stack them on top of each other.

```
/* styles.css */

.memory-card {
  width: calc(25% - 10px);
  height: calc(33.333% - 10px);
  margin: 5px;
  position: relative;
  box-shadow: 1px 1px 1px rgba(0,0,0,.3);
}

.front-face,
.back-face {
  width: 100%;
  height: 100%;
  padding: 20px;
  position: absolute;
  border-radius: 5px;
  background: #1C7CCC;
}
```
The template should be looking like this:

//TODO añadir pantallazo de este estado

### 🍿 Animando el cotarro
Let’s also add a click effect. The `:active` pseudo class will be triggered every time the element gets clicked and will apply a `.2s transition` to its size:

```
.memory-card {
  width: calc(25% - 10px);
  height: calc(33.333% - 10px);
  margin: 5px;
  position: relative;
  transform-style: preserve-3d;
  box-shadow: 1px 1px 0 rgba(0, 0, 0, .3);
  transform: scale(1);
}

 .memory-card:active {
   transform: scale(0.97);
   transition: transform .2s;
 }
 ```

### 👋 Añadir cursor custom

```
/* styles.css */

body {
  height: 100vh;
  display: flex;
  cursor: url('./assets/cursor.cur'), auto;
}

```

### 🩴 Flip card
To flip the card when clicked, a class flip will be added to the element. For that, let’s select all memory-card elements with `document.querySelectorAll`, loop through them with forEach and attach an event listener. 
Every time a card gets clicked flipCard function will be fired. The this variable represents the card that was clicked. 
The function accesses the element’s classList and toggles the flip class:

```
// scripts.js
const cards = document.querySelectorAll('.memory-card');

function flipCard() {
  this.classList.toggle('flip');
}

cards.forEach(card => card.addEventListener('click', flipCard));
```

In the CSS the flip class rotates the card 180deg:

```
.memory-card.flip {
  transform: rotateY(180deg);
}
```
To produce the 3D flip effect, we will add the perspective property to `.memory-game`. That property sets how far in the `z` plane the object is from the user. The lower the value the bigger the perspective effect. For a subtle effect, let’s apply `1000px`:

```
/* styles.css */

.memory-game {
  width: 640px;
  height: 640px;
  margin: auto;
  display: flex;
  flex-wrap: wrap;
  perspective: 1000px;
}
```
To the `.memory-card` elements let’s add `transform-style: preserve-3d`, to position them in the 3D space created in the parent, instead of flattening it to the `z = 0` plane (`transform-style`).

```
/* styles.css */

.memory-card {
  width: calc(25% - 10px);
  height: calc(33.333% - 10px);
  margin: 5px;
  position: relative;
  box-shadow: 1px 1px 1px rgba(0,0,0,.3);
  transform: scale(1);
  transform-style: preserve-3d;
}
```
Now, a transition has to be applied to the `transform` property to produce the movement effect:

```
/* styles.css */

.memory-card {
  width: calc(25% - 10px);
  height: calc(33.333% - 10px);
  margin: 5px;
  position: relative;
  box-shadow: 1px 1px 1px rgba(0,0,0,.3);
  transform: scale(1);
  transform-style: preserve-3d;
  transition: transform .5s;
}
```
### 🌍 3D flip
So, we got the card to 3D flip, yay! But why isn’t the card face showing up? Right now, both .front-face and .back-face are stacked up onto each other, because they are absolutely positioned. Every element has a back face, which is a mirror image of its front face. The property backface-visibility defaults to visible, so when we flip the card, what we get is the JS badge back face.

//TODO añadir animacion de carta girando

To reveal the image underneath it, let’s apply `backface-visibility: hidden` to `.front-face` and `.back-face`.

```
/* styles.css */

.front-face,
.back-face {
  width: 100%;
  height: 100%;
  padding: 20px;
  position: absolute;
  border-radius: 5px;
  background: #1C7CCC;
  backface-visibility: hidden;
}
```

Since we’ve hidden both images back face, there is nothing in the other side. So now we have to turn the `.front-face` 180 degrees:

```
.front-face {
  transform: rotateY(180deg);
}
```

And now, there’s the desired flip effect!

//TODO animación giro cartas


### 🧩 Assets para nuestro jueguico
- Los assets originales los podéis encontrar en mi perfil de Community de Figma
- En la carpeta assets en formato `.png` y `.svg`
- SVGOMG para optimizar los `.svg`

### 🏴‍☠️ Enlace del jueguico en codepen
- Proyecto en [codepen](https://codepen.io/carmenansio/pen/OJZMBwq/c9a3da5deb777c337616360afb27e8a2)
### 👾 Enlaces con Jueguitos Web
- Jamie-Coulter en [codepen](https://trost.notion.site/trost/Jamie-Coulter-s-CodePen-Gameshttps-codepen-io-jcoulterdesign-full-NeOQzX-1827d229ceea47cea1255c195c95d78d)
- Alvaro Montoro [CSSimon](https://codepen.io/alvaromontoro/pen/BaxKqwO)
