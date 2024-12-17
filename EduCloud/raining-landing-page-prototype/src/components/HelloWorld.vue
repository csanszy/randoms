<template>
  <!--
  <div class="bg">
    <div>
      <canvas ref="canvas" style="position: absolute; top: 0; left: 0;"></canvas>

      <div class="card">
        <button type="button" @click="toggleRain">Press me</button>
      </div>
    </div>
  </div> -->
  <canvas ref="canvas" style="position: absolute; top: 0; left: 0;"></canvas>

  <div class="containerr grid grid-cols-[25dvw_50dvw_25dvw] grid-rows-none">
    <div id="leftSide" class="fixed-top-right text-xl">
        <ul class=" flex space-x-4">
      <li>
        <RouterLink to="listing" class="text-black">Megtekintés</RouterLink>
      </li>
      <li>
        <router-link to="login" class="text-black">Bejelentkezés</router-link>
      </li>
      <li>
        <router-link to="admin/modules-create"  class="text-black">Admin</router-link>
      </li>
    </ul>
    </div>

    <div class="fixed-bottom-right">
      <button class="rain-button" @click="toggleRain"><img src="/required-stack/imgs/cloud-icon.png" alt="Button Image" /></button>
    </div>

    <div class="flex justify-end " id="rightSide">
        <div class="fixed-bottom-left font-semibold">
      <h1>EduCloud</h1>
    </div>
    </div>
</div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount, watch } from 'vue';

// Reactive state for rain effect toggle
const isRain = ref(false);
let counter = 0

// Function to toggle rain
const toggleRain = () => {
  if(counter == 0)  {
    initCanvas();
    counter++
  }
  if(isRain.value == false){
    isRain.value = true
  } else {
    isRain.value = false
  }
};

// Reference to canvas element using Vue's ref
const canvas = ref(null);
let ctx = null;
let width = 0;
let height = 0;

// Mouse position object
let mouse = { X: 0, Y: 0 };

// Particles and drops arrays
let particules = [];
let gouttes = [];

// Control settings for the animation
let controls = {
  rain: 2,
  Object: 'Nothing',
  alpha: 1,
  color: 200,
  auto: false,
  opacity: 1,
  saturation: 100,
  lightness: 50,
  back: 100,
  red: 0,
  green: 0,
  blue: 0,
  multi: false,
  speed: 2,
};

// Define requestAnimationFrame with fallback for compatibility
let requestAnimFrame = (function () {
  return (
    window.requestAnimationFrame ||
    window.webkitRequestAnimationFrame ||
    window.mozRequestAnimationFrame ||
    window.oRequestAnimationFrame ||
    window.msRequestAnimationFrame ||
    function (callback) {
      window.setTimeout(callback, 1000 / 60);
    }
  );
})();

// Function to create raindrops
const Rain = (X, Y, nombre) => {
  if (!nombre) nombre = 2;
  while (nombre--) {
    particules.push({
      vitesseX: Math.random() * 0.25,
      vitesseY: Math.random() * 9 + 1,
      X,
      Y,
      alpha: 1,
      couleur: `hsla(${controls.color},${controls.saturation}%,${controls.lightness}%,${controls.opacity})`,
    });
  }
};

// Function to create explosion of drops
const explosion = (X, Y, couleur, nombre) => {
  if (!nombre) nombre = 5;
  while (nombre--) {
    gouttes.push({
      vitesseX: Math.random() * 4 - 2,
      vitesseY: Math.random() * -4,
      X,
      Y,
      radius: 0.65 + Math.floor(Math.random() * 1.6),
      alpha: 1,
      couleur,
    });
  }
};

// Update the particles and raindrops
const update = () => {
  let particuleslocales = particules;
  let goutteslocales = gouttes;

  // Update particle positions
  for (let i = 0; i < particuleslocales.length; i++) {
    let particulesactives = particuleslocales[i];
    particulesactives.X += particulesactives.vitesseX;
    particulesactives.Y += particulesactives.vitesseY + 5;
    if (particulesactives.Y > height - 15) {
      particuleslocales.splice(i--, 1);
      explosion(particulesactives.X, particulesactives.Y, particulesactives.couleur);
    }
  }

  // Update drop positions
  for (let i = 0; i < goutteslocales.length; i++) {
    let gouttesactives = goutteslocales[i];
    gouttesactives.X += gouttesactives.vitesseX;
    gouttesactives.Y += gouttesactives.vitesseY;
    gouttesactives.radius -= 0.075;
    if (gouttesactives.alpha > 0) {
      gouttesactives.alpha -= 0.005;
    } else {
      gouttesactives.alpha = 0;
    }
    if (gouttesactives.radius < 0) {
      goutteslocales.splice(i--, 1);
    }
  }

  let i = controls.rain;
  while (i--) {
    Rain(Math.floor(Math.random() * width), -15);
  }
};

// Rendering the particles and raindrops
const rendu = (ctx) => {
  ctx.save();
  ctx.clearRect(0, 0, width, height); // Clear the entire canvas

  // Draw rain particles
  for (let particulesactives of particules) {
    ctx.globalAlpha = particulesactives.alpha;
    ctx.fillStyle = particulesactives.couleur;
    ctx.fillRect(particulesactives.X, particulesactives.Y, particulesactives.vitesseY / 4, particulesactives.vitesseY);
  }

  // Draw drops
  for (let gouttesactives of gouttes) {
    ctx.globalAlpha = gouttesactives.alpha;
    ctx.fillStyle = gouttesactives.couleur;
    ctx.beginPath();
    ctx.arc(gouttesactives.X, gouttesactives.Y, gouttesactives.radius, 0, Math.PI * 2);
    ctx.fill();
  }

  ctx.restore();
};

// Animation loop using requestAnimationFrame
const animate = () => {
  requestAnimFrame(animate);
  update();
  rendu(ctx);
};

// Initialize the canvas and set up the context and event listeners
const initCanvas = () => {
  if (canvas.value) {
    ctx = canvas.value.getContext('2d');
    width = canvas.value.width = window.innerWidth;
    height = canvas.value.height = window.innerHeight;
    window.onresize = () => {
      width = canvas.value.width = window.innerWidth;
      height = canvas.value.height = window.innerHeight;
    };
    window.onmousemove = (event) => {
      mouse.X = event.clientX;
      mouse.Y = event.clientY;
    };
    animate();
  }
};
const cleanupCanvas = () => {
  // Stop the animation by cancelling the requestAnimationFrame
  if (animationFrameId) {
    cancelAnimationFrame(animationFrameId); // Stop the ongoing animation frame
    animationFrameId = null;  // Clear the animation frame ID
  }

  // Clear particles and drops to stop the rain effect
  particules = [];
  gouttes = [];

  // Clear the canvas if ctx exists
  if (ctx) {
    ctx.clearRect(0, 0, width, height); // Clear the entire canvas
  }
};
// Watch for rain toggle and update accordingly
watch(isRain, (newVal) => {
  if (newVal) {
    // Trigger rain when isRain is true
    controls.rain = 12;  // Adjust intensity as needed
  } else {
    controls.rain = 0;  // Stop rain when isRain is false
  }
});

onBeforeUnmount(() => {
  // Cleanup if needed
});
</script>

<style scoped>

.rain-button {
  background-color: transparent; /* Ha átlátszó hátteret szeretnél */
  border: none; /* Távolítsd el az alapértelmezett szegélyt */
  padding: 0; /* Távolítsd el az alapértelmezett margót és paddinget */
  cursor: pointer; /* Mutassa, hogy kattintható */
}

.rain-button img {
  width: 7vw; /* Kép szélessége */
  height: 7vw; /* Magasság automatikusan arányos lesz */
  display: block; 
}

.fixed-bottom-left {
  position: fixed;
  bottom: 0;
  left: 0;
  margin: 3%;
  color: black;
}

.fixed-bottom-right {
  position: fixed;
  bottom: 0;
  right: 0;
  margin: 3%;
  color: black;
}
h1{
    font-size: 17vh;
    font-family: Verdana;
    margin: 0;
    line-height: 1;
    transition: 0.3s;
}

@media (max-width: 1000px) {
    h1{
      font-size: 12vh;
  }
}

@media (max-width: 710px) {
    h1{
      font-size: 8vh;
  }
}

@media (max-width: 430px) {
    h1{
      font-size: 5vh;
  }
}

.fixed-top-right {
  position: fixed;
  top: 0;
  right: 0;
  margin: 2%;
  margin-right: 3%;
  color: black;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  display: inline;
}

.router-link {
  text-decoration: underline;
}

</style>
