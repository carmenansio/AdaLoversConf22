## AdaLoversConf22-WIP

En este tutorial veremos conceptos básico de HTML, CSS y JS. Tocaremos transiciones, data-attributes, flexbox... no hace falta ser una experta para seguir este tutorial, si sabéis que estos lenguajes web existen, es todo lo que se necesita 🤘

### Estructura de archivos

Estos son los archivos necesarios para nuestro proyecto:

1. Creamos la carpeta de `memory-game`
2. Entramos en la carpeta creada
3. Dentro generamos los archivos `index.html` `styles.css` `scripts.js`
4. Creamos la carpeta `assets` 

🎸  mkdir memory-game
🎸  cd memory-game
🎸  touch index.html styles.css scripts.js
🎸  mkdir assets

### En nuestro HTML
En el archivo `index.html` tenemos que linkar los dos archivos que hemos creeado, el `styles.css` y el `scripts.js`.

<!-- index.html -->
`
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
`
