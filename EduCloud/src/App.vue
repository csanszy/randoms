<script setup>
</script>

<template>
  <div class="bg-container">
    <RouterView/>
  </div>
</template>

<style scoped>
.bg-container {
  overflow: hidden;
  background-image: url('../../EduCloud/src/imgs/night.jpg');
  background-repeat: no-repeat;
  background-position: center center;
  background-size: cover;
  width: 100%;
  height: 100vh; 
  mix-blend-mode: var(--_mesh-gradient-blend-mode);
}

@media (max-width: 768px) {
  .bg-container {
    background-size: cover; 
    background-position: top center;
  }
}

@media (max-width: 480px) {
  .bg-container {
    background-size: cover; 
    background-position: center center; 
  }
}
</style>
