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

### 🍿 Animando el cotarro
//TODO añadir la clase .active
//TODO añadir las transiciones entre front y back (flip card)
### 🧩 Assets para nuestro jueguico
- Los assets originales los podéis encontrar en mi perfil de Community de Figma
- En la carpeta assets en formato `.png` y `.svg`
- SVGOMG para optimizar los `.svg`

### 🏴‍☠️ Enlace del jueguico en codepen
- Proyecto en [codepen](https://codepen.io/carmenansio/pen/OJZMBwq/c9a3da5deb777c337616360afb27e8a2)
### 👾 Enlaces con Jueguitos Web
- Jamie-Coulter en [codepen](https://trost.notion.site/trost/Jamie-Coulter-s-CodePen-Gameshttps-codepen-io-jcoulterdesign-full-NeOQzX-1827d229ceea47cea1255c195c95d78d)
- Alvaro Montoro [CSSimon](https://codepen.io/alvaromontoro/pen/BaxKqwO)
