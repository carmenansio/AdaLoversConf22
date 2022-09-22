# 💃 AdaLoversConf22
👋 Hola!! Las **slides** del Workshop las tenéis [aquí](./memory-game/assets/slides/slides.pdf)
### 🎁 Repositorio del Workshop "Desarrolla tu primer videojuego"

En este tutorial veremos conceptos básico de `HTML`, `CSS` y `JS`. Tocaremos `transiciones`, `data-attributes`, `flexbox`...**no hace falta ser una experta** para seguir este tutorial, si sabéis que estos lenguajes web existen, es todo lo que se necesita 🤘.

(PD: vamos a jugar con `vanilla` tanto en `css` como en `js`. **No utilizaremos** ni precompiladores como `SASS`, ni frameworks como `Tailwind`,ni `TypeScript`.)

![Super Mario Bros 3 intro](./memory-game/assets/media/intro.gif)

### 👏 Diseño y Desarrollo

La **interfaz del juego** se ha diseñado en `Figma`. Cada `item` es un componente con `variants` 👇

![Diseño del tablero](./memory-game/assets/figma-board.png)
![Diseño de los items](./memory-game/assets/figma-items.png)


### 🏗 Arquitectura de archivos

Estos son los **archivos necesarios** para nuestro proyecto:

1. Creamos la carpeta de `memory-game`
2. Entramos en la carpeta creada
3. Dentro generamos los archivos `index.html` `styles.css` `scripts.js`
4. Creamos la carpeta `assets` 

##### Cómo crear los archivos directamente en la consola:
- 1️⃣  mkdir memory-game
- 2️⃣  cd memory-game
- 3️⃣  touch index.html styles.css scripts.js
- 4️⃣  mkdir assets

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

### 🍱 Layout principal
Creamos el layout principal con un tag `section` en la estructura del `html`.

```
<!-- index.html -->
<section class="memory-game"></section>
```

![Board back](https://assets.codepen.io/527512/board-back.png)
![Board front](https://assets.codepen.io/527512/board-front.png)

### 🧩 Assets para nuestro jueguico
- Los assets originales los podéis encontrar en mi **perfil de Community de Figma**
- En la carpeta assets en formato `.png` y `.svg`
- `SVGOMG` para optimizar los `.svg`
- `ImageOptim` para optimizar las imágenes

### 🃏 Nuestro jueguico de cartas
El juego consta de **18 cartas**, cada una está creada por un `div` contenedor que hemos llamado `.memory-card`, el cuál tiene **dos imágenes** `SVG`. 
La primera imágen será la cara frontal `front-card` y **la segunda será común** a todas, con el logo original de **Nintendo** cómo `back-card`.

```
<!-- styles.css -->
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

### 💣 CSS al ataque
Utilizaremos un **reset** muy básico pero **efectivo** 👇

```
<!-- styles.css -->
/* reset */

* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
```

ℹ️ **Un poco de teoría**:

- El modelo de caja `box-sizing`: La propiedad `border-box` incluye los padding y valores de borders **dentro del tamaño total del elemento**, width y height. 🧮 Así **simplificamos los cálculos**.

- Indicando al `body` que tenga un `display: flex` a la clase `.memory-game` que actua cómo contenedor, creamos una alineación vertical y horizontal.

- La clase `.memory-game` también será un contenedor con comportamiento `flex-container`. Por defecto, los elementos vienen seteados con `shrink` en lo ancho para ajustarse al contenedor. Seteando `flex-wrap` con el valor `wrap`, los `flex-items` se posicionará  a lo largo de multiples lineas dependiendo de su propio tamaño.

```
<!-- styles.css -->

body {
  height: 100vh;
  display: flex;
}

.memory-game {
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-flow: row wrap;
  place-content: space-around;
  justify-content: center;
}
```
### 🍍 Dando estilo a nuestro jueguico
La altura y el ancho de cada carta está calculado con la función `calc()` de `CSS`, hemos creado `3 filas`, con **6 cartas en cada fila** con un `16.6%` y una altura de `33.3%` y **restamos 10px** para añadir el margen entre cartas.

Para poder posicionar los **hijos** del contenedor `.memory-card`, hemos añadido la propiedad `position: relative`, para poder posicionarlos de manera absoluta `position: absolute` y sean relativos al contenedor **madre**. 👇
**❓ ¿Se entiende este comportamiento?**

La propiedad `position: absolute` está indicada a ambas caras de las cartas `.front-card` y `.back-card` esto hará que los elementos salgan de su flujo normal y se posicionen una cara sobre otra.

```
<!-- styles.css -->

.memory-card {
  width: calc(16.666% - 10px);
  height: calc(33.333% - 10px);
  margin: 5px;
  position: relative;
}

.front-card,
.back-card {
  width: 100%;
  height: 100%;
  padding: 20px;
  position: absolute;
  border-radius: 10px;
  border: 3px solid var(--border);
}
```
![Board Nintendo](./memory-game/assets/board-nintendo.png)

### 🍿 Animando el cotarro
Vamos a añadir una micro interacción que simulará un `efecto click`. La pseudo clase `:active` actuará de trigger cada vez que el elemento sea clicado y aplicará una animación al tamaño de la carta con `.2s transition`. A la clase `.memory-card` le añadimos un `transform: scale(1)`.

```
<!-- styles.css -->

.memory-card {
  width: calc(16.666% - 10px);
  height: calc(33.333% - 10px);
  margin: 5px;
  position: relative;
  transform: scale(1);
}

 .memory-card:active {
   transform: scale(0.97);
   transition: transform .2s;
 }
 ```

### 👋 Añadir cursor custom
Hemos añadido la **manita de Mario** como cursor para simular que es él quién está seleccionando las cartas.

Podemos **crear un cursor custom** con la siguiente linea de código👇

```
<!-- styles.css -->

body {
  height: 100vh;
  display: flex;
  cursor: url('./assets/cursor.cur'), auto;
}
```
### 🩴 Flip card
Para crear el efecto de voltear la carta cada vez que sea clicada, vamos a añadir la clase `.flip`. Con un `document.querySelectorAll` seleccionamos todos los elementos del contenedor `memory-card` se genera un loop con cada `forEach` y le atacha un `event listener`. 

Cada vez que una carta sea clicada la `función flipCard` será ejecutada.
La variable `this` representa que la carta ha sido clicada. 

La función `flipCard()` accede a los elementos de `classList` y hace un `toggles` a la `flip class`:

```
<!-- scripts.js -->

const cards = document.querySelectorAll('.memory-card');

function flipCard() {
  this.classList.toggle('flip');
}

cards.forEach(card => card.addEventListener('click', flipCard));
```

La clase `.flip` rota la carta `180deg`:

```
.memory-card.flip {
  transform: rotateY(180deg);
}
```

Para producir el `efecto 3D`, añadimos una propiedad de perspectiva a la clase `.memory-game`. Esta propiedad define cuanto de lejos en el plano de `a` el objeto se alejará de nuestra vista.


Para un efecto `subtle` aplicamos a la perspectiva un valor de `1000px` añadiendo a la clase `.memory-game` la propiedad `perspective: 1000px;`:

```
<!-- styles.css -->

.memory-game {
   width: 100vw;
  height: 100vh;
  display: flex;
  flex-flow: row wrap;
  place-content: space-around;
  justify-content: center;
  perspective: 1000px;
}
```
To the `.memory-card` elements let’s add `transform-style: preserve-3d`, to position them in the 3D space created in the parent, instead of flattening it to the `z = 0` plane (`transform-style`).
Añadiendo la propiedad `transform-style: preserve-3d;`

```
<!-- styles.css -->

.memory-card {
  width: calc(16.666% - 10px);
  height: calc(33.333% - 10px);
  margin: 5px;
  position: relative;
  transform: scale(1);
  transform-style: preserve-3d;
}
```
Aplicamos una transición con la propiedad `transition: transform .5s;` para producir el efecto de movimiento:

```
<!-- styles.css -->

.memory-card {
  width: calc(16.666% - 10px);
  height: calc(33.333% - 10px);
  margin: 5px;
  position: relative;
  transform: scale(1);
  transform-style: preserve-3d;
  transition: transform .5s;
}
```
### 🌍 3D flip
So, we got the card to 3D flip, yay! But why isn’t the card face showing up?

Right now, both .front-face and `.back-face` are stacked up onto each other, because they are absolutely positioned. Every element has a back face, which is a mirror image of its front face. The property `backface-visibility` defaults to visible, so when we flip the card, what we get is the JS badge `back-face`.

To reveal the image underneath it, let’s apply `backface-visibility: hidden;` to `.front-face` and `.back-face`.

```
<!-- styles.css -->

.front-face,
.back-face {
  width: 100%;
  height: 100%;
  padding: 20px;
  position: absolute;
  border-radius: 10px;
  border: 3px solid var(--border);
  backface-visibility: hidden;
}
```

Since we’ve hidden both images back face, there is nothing in the other side. So now we have to turn the `.front-face` `180` grados con la propiedad `transform: rotateY(180deg);`:

```
<!-- styles.css -->

.front-face {
  transform: rotateY(180deg);
}
```

Ya tenemos controlado el giro!

![Giro de la carta](./memory-game/assets/media/flip-card.gif)

### 🧡 Encontrando la media naranja
El comportamiento/funcionalidad que queremos es:

- **Cuando hacemos clic en la primera carta**, debe esperar hasta que se gire la siguiente. 
- Las variables `hasFlippedCard` y `flippedCard` administrarán el `estado` de `flip`. 
- **En caso de que no haya una carta girada**, `hasflippedCard` está configurada en `True` y `flippedCard` está configurada a la tarjeta que ha tenido el clic.

También cambiamos el método `toggle` para agregar:

```
<!-- scripts.js -->

  const cards = document.querySelectorAll('.memory-card');

+ let hasFlippedCard = false;
+ let firstCard, secondCard;

  function flipCard() {
-   this.classList.toggle('flip');
+   this.classList.add('flip');

+   if (!hasFlippedCard) {
+     hasFlippedCard = true;
+     firstCard = this;
+   }
  }

cards.forEach(card => card.addEventListener('click', flipCard));
```
So now, when the user clicks the second card, we will fall into the else block in our condition. We will check to see if it’s a match. In order to do that, let’s identify each card.

Whenever we feel like adding extra information to HTML elements, we can make use of data attributes. By using the following syntax: data-*, where, * can be any word, that attribute will be inserted in the element’s dataset property. So, let’s add a `data-item` to each card:

```
<!-- index.html -->

+ <div class="memory-card" data-item="star">
```
So now we can check for a match by accessing both cards dataset. Let’s extract the matching logic to its own method checkForMatch() and also set hasFlippedCard back to false. In case of a match, disableCards() is invoked and the event listeners on both cards are detached, to prevent further flipping. Otherwise, unflipCards() will turn both cards back by a 1500ms timeout that removes the .flip class:

Putting all together:

```
<!-- scripts.js -->

const cards = document.querySelectorAll('.memory-card');

  let hasFlippedCard = false;
  let firstCard, secondCard;

  function flipCard() {
    this.classList.add('flip');

    if (!hasFlippedCard) {
      hasFlippedCard = true;
      firstCard = this;
+     return;
+   }
+
+   secondCard = this;
+   hasFlippedCard = false;
+
+   checkForMatch();
+ }
+
+ function checkForMatch() {
+   if (firstCard.dataset.framework === secondCard.dataset.framework) {
+     disableCards();
+     return;
+   }
+
+   unflipCards();
+ }
+
+ function disableCards() {
+   firstCard.removeEventListener('click', flipCard);
+   secondCard.removeEventListener('click', flipCard);
+ }
+
+ function unflipCards() {
+   setTimeout(() => {
+     firstCard.classList.remove('flip');
+     secondCard.classList.remove('flip');
+   }, 1500);
+ }

  cards.forEach(card => card.addEventListener('click', flipCard));

```
### 🎩 Con un ternarío 
A more elegant way of writing the matching condition is to use a ternary operator. It’s composed by three blocks. The first block is the condition to be evaluated. The second block is executed if the condition returns true, otherwise the executed block is the third:

```
<!-- scripts.js -->

- if (firstCard.dataset.name === secondCard.dataset.name) {
-   disableCards();
-   return;
- }
-
- unflipCards();

+ let isMatch = firstCard.dataset.name === secondCard.dataset.name;
+ isMatch ? disableCards() : unflipCards();
```
## 💎 Corner cases
### Lock Board
So now that we have the matching logic covered, we need to lock the board. We lock the board to avoid two sets of cards being turned at the same time, otherwise the flipping will fail.

Let’s declare a lockBoard variable. When the player clicks the second card, lockBoard will be set to true and the condition if (lockBoard) return; will prevent any card flipping before the cards are hidden or match:

```
<!-- scripts.js -->

const cards = document.querySelectorAll('.memory-card');

  let hasFlippedCard = false;
+ let lockBoard = false;
  let firstCard, secondCard;

  function flipCard() {
+   if (lockBoard) return;
    this.classList.add('flip');

    if (!hasFlippedCard) {
      hasFlippedCard = true;
      firstCard = this;
      return;
    }

    secondCard = this;
    hasFlippedCard = false;

    checkForMatch();
  }

  function checkForMatch() {
    let isMatch = firstCard.dataset.name === secondCard.dataset.name;
    isMatch ? disableCards() : unflipCards();
  }

  function disableCards() {
    firstCard.removeEventListener('click', flipCard);
    secondCard.removeEventListener('click', flipCard);
  }

  function unflipCards() {
+     lockBoard = true;

    setTimeout(() => {
      firstCard.classList.remove('flip');
      secondCard.classList.remove('flip');

+     lockBoard = false;
    }, 1500);
  }

  cards.forEach(card => card.addEventListener('click', flipCard));
```

### Same Card Click
The is still the case where the player can click twice on the same card. The matching condition would evaluate to true, removing the event listener from that card.

To prevent that, let’s check if the current clicked card is equal to the firstCard and return if positive.

```
<!-- scripts.js -->

if (this === firstCard) return;
```

The `firstCard` and `secondCard` variables need to be reset after each round, so let’s extract that to a new method `resetBoard()`. Let’s place the `hasFlippedCard = false;` and `lockBoard = false` there too. The es6 destructuring assignment `[var1, var2] = ['value1', 'value2']`, allows us to keep the code super short:

```
<!-- scripts.js -->

function resetBoard() {
  [hasFlippedCard, lockBoard] = [false, false];
  [firstCard, secondCard] = [null, null];
}
```

The new method will be called both from `disableCards()` and `unflipCards()`:

```
<!-- scripts.js -->

const cards = document.querySelectorAll('.memory-card');

  let hasFlippedCard = false;
  let lockBoard = false;
  let firstCard, secondCard;

  function flipCard() {
    if (lockBoard) return;
+   if (this === firstCard) return;

    this.classList.add('flip');

    if (!hasFlippedCard) {
      hasFlippedCard = true;
      firstCard = this;
      return;
    }

    secondCard = this;
-   hasFlippedCard = false;

    checkForMatch();
  }

  function checkForMatch() {
    let isMatch = firstCard.dataset.name === secondCard.dataset.name;
    isMatch ? disableCards() : unflipCards();
  }

  function disableCards() {
    firstCard.removeEventListener('click', flipCard);
    secondCard.removeEventListener('click', flipCard);

+   resetBoard();
  }

  function unflipCards() {
    lockBoard = true;

    setTimeout(() => {
      firstCard.classList.remove('flip');
      secondCard.classList.remove('flip');

-     lockBoard = false;
+     resetBoard();
    }, 1500);
  }

+ function resetBoard() {
+   [hasFlippedCard, lockBoard] = [false, false];
+   [firstCard, secondCard] = [null, null];
+ }

  cards.forEach(card => card.addEventListener('click', flipCard));
```
### Shuffling
Our game looks pretty good, but there is no fun if the cards are not shuffled, so let’s take care of that now.

When display: flex is declared on the container, flex-items are arranged by the following hierarchy: group and source order. Each group is defined by the order property, which holds a positive or negative integer. By default, each flex-item has its order property set to 0, which means they all belong to the same group and will be laid out by source order. If there is more than one group, elements are firstly arranged by ascending group order.

There is 12 cards in the game, so we will iterate through them, generate a random number between 0 and 12 and assign it to the flex-item order property:

```
<!-- scripts.js -->

function shuffle() {
  cards.forEach(card => {
    let ramdomPos = Math.floor(Math.random() * 12);
    card.style.order = ramdomPos;
  });
}
```
In order to invoke the shuffle function, let’s make it a Immediately Invoked Function Expression (IIFE), which means it will execute itself right after its declaration. The scripts should look like this:

```
<!-- scripts.js -->

const cards = document.querySelectorAll('.memory-card');

  let hasFlippedCard = false;
  let lockBoard = false;
  let firstCard, secondCard;

  function flipCard() {
    if (lockBoard) return;
    if (this === firstCard) return;

    this.classList.add('flip');

    if (!hasFlippedCard) {
      hasFlippedCard = true;
      firstCard = this;
      return;
    }

    secondCard = this;
    lockBoard = true;

    checkForMatch();
  }

  function checkForMatch() {
    let isMatch = firstCard.dataset.name === secondCard.dataset.name;
    isMatch ? disableCards() : unflipCards();
  }

  function disableCards() {
    firstCard.removeEventListener('click', flipCard);
    secondCard.removeEventListener('click', flipCard);

    resetBoard();
  }

  function unflipCards() {
    setTimeout(() => {
      firstCard.classList.remove('flip');
      secondCard.classList.remove('flip');

      resetBoard();
    }, 1500);
  }

  function resetBoard() {
    [hasFlippedCard, lockBoard] = [false, false];
    [firstCard, secondCard] = [null, null];
  }

+ (function shuffle() {
+   cards.forEach(card => {
+     let ramdomPos = Math.floor(Math.random() * 12);
+     card.style.order = ramdomPos;
+   });
+ })();

  cards.forEach(card => card.addEventListener('click', flipCard));
```
### 🙌 YA LO TENEMOS

### 🏴‍☠️ Enlace del jueguico en codepen
- Proyecto en [codepen](https://codepen.io/carmenansio/pen/OJZMBwq/c9a3da5deb777c337616360afb27e8a2)
### 👾 Gente que hace Jueguitos Web
- Jamie-Coulter en [codepen](https://trost.notion.site/trost/Jamie-Coulter-s-CodePen-Gameshttps-codepen-io-jcoulterdesign-full-NeOQzX-1827d229ceea47cea1255c195c95d78d)
- Alvaro Montoro [CSSimon](https://codepen.io/alvaromontoro/pen/BaxKqwO)
