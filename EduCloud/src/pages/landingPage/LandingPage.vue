<script setup lang="ts">

  

</script>

<template>
  <link href='https://unpkg.com/boxicons@2.1.4/css/boxicons.min.css' rel='stylesheet'>
  <div class="containerr h-[100dvh] w-[100dvw]">

  <header class="header">

    <input type="checkbox" id="check">
      <label for="check" class="icons">
        <i class='bx bx-menu' id="menu-icon"></i>
        <i class='bx bx-x' id="close-icon"></i>
      </label>

      <head>
        <title>EduCloud</title>
      </head> 

      <nav class="navbar flex flex-col float-right md:flex-row mr-5 mt-5 md:space-x-4">
        <a>
          <router-link style="--i:0" to="listing" class="asd text-white hover:underline">Megtekintés</router-link>
        </a>
        <a>
          <router-link style="--i:1" to="login" class="text-white hover:underline">Bejelentkezés</router-link>
        </a>
        <a>
          <router-link style="--i:2" to="admin/modules-create" class="text-white hover:underline">Admin</router-link>
        </a>
      </nav>

    </header>

  </div>

    <div class="flex justify-end " id="rightSide">
        <div class="fixed-bottom-left font-semibold">
      <h1>EduCloud</h1>
    </div>
    </div>
</template>

<style scoped>

.header{
    position: fixed;
    width: 100%;
    justify-content: space-between;
    z-index: 100;
    padding: 1.3rem;
}

.header::before{
    z-index: -12;
}

.table {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background-color: rgba(0, 0, 0, 0.1);
    backdrop-filter: blur(50px);
    width: 70%;
    height: 60%;
    margin-top: -3%;
    border-radius: 10px;
}

.navbar a{
    font-size: 1.15rem;
    color: rgb(255, 255, 255);
    text-decoration: none;transition: 0.3s;
    text-shadow: 0 0 2px #000000;
}


.navbar a:hover, .navbar a:active,.navbar a:focus{
    transform: translateY(-1px);
    text-decoration: underline;
}

#check{
    display: none;
}

.icons{
    right: 3%;
    position: absolute;
    font-size: 2.8rem;
    cursor: pointer;
    color:white;
    display: none;
}

@media (max-width: 992px){
    .header{
        padding: 1.3rem 5%;
    }
}

@media (max-width: 910px){
    .icons{
        display: inline-flex;
    }

    #check:checked~.icons #menu-icon{
        display: none;
    }

    .icons #close-icon{
        display: none;
    }

    #check:checked~.icons #close-icon{
        display: block;
    }

    .navbar{
        display: flex;
        flex-direction: column;
        position: absolute;
        top: 100%;
        left: 0;
        width: 100%;
        overflow: hidden;
        transition: all 0.3s ease;
    }

    #check:checked~.navbar{
        height: 13.8rem;
    }

    .navbar a{
        display: block;
        font-size: 1.1rem;
        margin: .3rem 0;
        text-align: center;
        opacity: 0;
        transform: translateY(-50px);
        transition: all 0.13s ease;
    }

    #check:checked~.navbar a{
        transform: translateY(0);
        opacity: 12;
        transition-delay: calc(.1s * var(--i));
    }

}

.fixed-bottom-left {
  position: fixed;
  bottom: 0;
  left: 0;
  margin: 3%;
}
h1{
    font-size: 17vh;
    font-family: Verdana;
    margin: 0;
    line-height: 1;
    transition: 0.3s;
    color: #ffffff;
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
.containerr {
  background: url('../../../imgs/night.jpg') no-repeat center center;
  background-size: cover;
  mix-blend-mode: var(--_mesh-gradient-blend-mode);
  
}
@media (max-width: 768px) {
  .containerr {
    background: url('/courseController/SZF1_13_Frontend_CourseController/CourseController/src/Views/LandingPage/képek/nightWest.jpg') no-repeat center center;
    background-size: cover;
  }
}

@media (max-width: 480px) {
  .containerr {
    background-position: top;
    background-size: contain;
  }
}

</style>