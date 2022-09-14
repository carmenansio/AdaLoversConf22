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
El juego tiene 16 cartas, cada una está creada por un `div` contenedor que hemos llamado `.memory-card`, el cuál tiene dos imágenes `SVG`. La primera imágen será la cara frontal `front-card` y la segunda será común a todas, con el logo original de Nintendo cómo `back-card`.

```
<div class="memory-card">
  <img class="front-card" src="img/flower-snow.svg" alt="Flor de Nieve">
  <img class="back-card" src="img/nintendo.svg" alt="Logo de Nintendo">
</div>
```

### 🧩 Assets para nuestro jueguico
Los assets originales los podéis encontrar en mi perfil de Community de Figma
