<script setup lang="ts">
import { onMounted } from 'vue';

const swiperCss = document.createElement('link');
swiperCss.rel = 'stylesheet';
swiperCss.href = 'https://unpkg.com/swiper@8/swiper-bundle.min.css';
document.head.appendChild(swiperCss);

onMounted(() => {

  const ioniconsScript = document.createElement('script');
  ioniconsScript.type = 'module';
  ioniconsScript.src = 'https://unpkg.com/ionicons@5.5.2/dist/ionicons/ionicons.esm.js';
  document.head.appendChild(ioniconsScript);

  const ioniconsNomoduleScript = document.createElement('script');
  ioniconsNomoduleScript.noModule = true;
  ioniconsNomoduleScript.src = 'https://unpkg.com/ionicons@5.5.2/dist/ionicons/ionicons.js';
  document.head.appendChild(ioniconsNomoduleScript);

  const swiperScript = document.createElement('script');
  swiperScript.src = 'https://unpkg.com/swiper@8/swiper-bundle.min.js';
  document.head.appendChild(swiperScript);

  swiperScript.onload = () => {

    new Swiper('.tranding-slider', {
      effect: 'coverflow',
      grabCursor: true,
      centeredSlides: true,
      loop: true,
      slidesPerView: 'auto',
      coverflowEffect: {
        rotate: 0,
        stretch: 0,
        depth: 100,
        modifier: 2.5,
      },
      pagination: {
        el: '.swiper-pagination',
        clickable: true,
      },
      navigation: {
        nextEl: '.swiper-button-next',
        prevEl: '.swiper-button-prev',
      }
    });
  };
});

// Function to navigate to different pages
const navigateToPage = (url: string) => {
  window.location.href = url;
};
</script>

<template>
  <section id="tranding">
    <div class="container">
      <h1 class="text-center section-heading">Szakmák</h1>
    </div>
    <div class="container">
      <div class="swiper tranding-slider">
        <div class="swiper-wrapper">
          <div class="swiper-slide tranding-slide">
            <div class="tranding-slide-img">
              <img src="../../imgs/szoftver.jpg" alt="Tranding">
            </div>
            <div class="tranding-slide-content">
              <h2 class="szakma-name">
                Szoftverfejlesztő és -tesztelő
              </h2><br>
              <div class="button-container">
                <button @click="navigateToPage('/szoftverfejleszto')">
                  <ion-icon name="arrow-forward-outline"></ion-icon>
                </button>
              </div>
            </div>
          </div>

          <div class="swiper-slide tranding-slide">
            <div class="tranding-slide-img">
              <img src="../../imgs/rendszeruzemelteto.jpg" alt="Tranding">
            </div>
            <div class="tranding-slide-content">
              <h2 class="szakma-name long" >
                Informatikai rendszer- és alkalmazás-üzemeltető technikus
              </h2><br>
              <div class="button-container">
                <button @click="navigateToPage('/rendszeruzemelteto')">
                  <ion-icon name="arrow-forward-outline"></ion-icon>
                </button>
              </div>
            </div>
          </div>

          <div class="swiper-slide tranding-slide">
            <div class="tranding-slide-img">
              <img src="../../imgs/elektro.jpg" alt="Tranding">
            </div>
            <div class="tranding-slide-content">
              <h2 class="szakma-name">
                Erősáramú elektrotechnikus
              </h2><br>
              <div class="button-container">
                <button @click="navigateToPage('/elektro')">
                  <ion-icon name="arrow-forward-outline"></ion-icon>
                </button>
              </div>
            </div>
          </div>

          <div class="swiper-slide tranding-slide">
            <div class="tranding-slide-img">
              <img src="../../imgs/automatikaiTechnikus.jpg" alt="Tranding">
            </div>
            <div class="tranding-slide-content">
              <h2 class="szakma-name">
                Automatikai technikus
              </h2><br>
              <div class="button-container">
                <button @click="navigateToPage('/automatikai-technikus')">
                  <ion-icon name="arrow-forward-outline"></ion-icon>
                </button>
              </div>
            </div>
          </div>

          <div class="swiper-slide tranding-slide">
            <div class="tranding-slide-img">
              <img src="../../imgs/kozismeret.jpg" alt="Tranding">
            </div>
            <div class="tranding-slide-content">
              <h2 class="szakma-name">
                Közismeret
              </h2><br>
              <div class="button-container">
                <button @click="navigateToPage('/kozismeret')">
                  <ion-icon name="arrow-forward-outline"></ion-icon>
                </button>
              </div>
            </div>
          </div>
        </div>

        <div class="tranding-slider-control">
          <div class="swiper-button-prev slider-arrow">
          </div>
          <div class="swiper-pagination"></div>
          <div class="swiper-button-next slider-arrow">
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>

button {
  width: 50px;
  height: 50px;
  background-color: #ec994b;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  color: var(--white);
  border: none;
  cursor: pointer;
  filter: drop-shadow(0px 0px 5px #ec994b);
  transition: .3s;
}

button:hover{
  filter: drop-shadow(0px 0px 15px #000000);
}

button ion-icon {
  font-size: 1.5rem;
}

:root {
  --primary: #ec994b;
  --white: #ffffff;
  --bg: #f5f5f5;
  --slider-bg: #222224;
}

*,
*::before,
*::after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  list-style-type: none;
  text-decoration: none;
}

html {
  font-family: "Montserrat", sans-serif;
}

body {
  font-size: 1.6rem;
  background-color: var(--bg);
}

.container {
  max-width: 124rem;
  padding: 0 7.1rem;
  margin: 0 auto;
}

.text-center {
  text-align: center;
}

.section-heading {
  font-size: 3rem;
  color: white;
  padding-bottom: 2rem;
  font-weight: bold; 
  text-transform: uppercase; 
}

#tranding {
  padding: 4rem 0;
  background-color: var(--slider-bg);
  border-radius: 15px;
}

#tranding .tranding-slider {
  max-width: 100dvw;
  min-width: 55dvw;
  height: 50rem;
  padding: 1rem 0;
  position: relative;
  border-radius: 15px;
}


@media (max-width:500px) {
  #tranding .tranding-slider {
    height: 45rem;
    width: 22rem;
    left: -80px;
  }

  .text-center{
  }

  .tranding-slide {
    width: 20rem !important;
    height: 22rem !important;
  }

  .szakma-name {
    font-size: .5rem;
  }
}

@media (max-width: 900px) {
  .tranding-slider {
    height: 45rem;
  }

  #tranding .tranding-slider {
    width: 57rem;
    left: -114px;
  }

  .tranding-slide {
    height: 5rem;
    width: 22rem;
  }
}

.tranding-slide .tranding-slide-img {
  flex: 2; 
}

.tranding-slide .tranding-slide-img img {
  width: 100%;
  height: 100%; 
  object-fit: cover;
  border-radius: 1.5rem 1.5rem 0 0; 
}

.tranding-slide .tranding-slide-content {
  flex: 1; 
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  text-align: center;
  border-radius: 0 0 1.5rem 1.5rem; 
  padding: 1rem;
  position: relative;
}

.tranding-slide {
  width: 30rem;
  height: 32rem;
  position: relative;
  border-radius: 1.5rem;
  overflow: auto;
  box-shadow: 0 10px 30px rgb(0, 0, 0);
  background-color: rgba(255, 255, 255, 0.219);
  backdrop-filter: blur(50px);
  display: flex;
  flex-direction: column; 
  margin: 0 auto; 
}

.szakma-name {
  font-size: 1.8rem;
  font-weight: bold;
}

.swiper-slide-shadow-left,
.swiper-slide-shadow-right {
  display: none;
}

.tranding-slider-control {
  position: absolute;
  bottom: 150px; 
  display: flex;
  justify-content: space-between; 
  align-items: center;
  width: 100%;
  padding: 0 2rem; 
}

.swiper-pagination {
  display: flex;
  justify-content: center; 
}

.swiper-pagination .swiper-pagination-bullet {
  width: 2rem;
  height: 2rem;
  background: var(--white);
  opacity: 0.8;
  transition: all 0.3s ease;
}

.swiper-pagination .swiper-pagination-bullet-active {
  background: var(--primary);
}

.swiper-button-prev, 
.swiper-button-next {
  color: white;
  padding: 10px;
  border-radius: 50%;
}

.button-container {
  position: absolute;
  bottom: 10px; 
  right: 10px;
}

.swiper-button-prev, 
.swiper-button-next {
  color: white;
  padding: 10px;
  border-radius: 50%;
  position: absolute;
  top: 50%; 
  transform: translateY(-50%); 
}

.swiper-button-prev {
  left: 10px; 
}

.swiper-button-next {
  right: 10px; 
}


</style>
