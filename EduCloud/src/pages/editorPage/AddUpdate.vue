<template>
  <div
    class="editor-container"
    :style="{ backgroundImage: `url(${currentBackground})` }"
  >
    <div class="nav-bar">
      <button class="back-button">←</button>
      <span class="title">Szerkesztés</span>
      <div class="user-dropdown">
        <button class="user-button" @click="toggleDropdown">👤</button>
        <div v-if="dropdownVisible" class="dropdown-menu">
          <button class="dropdown-item" @click="toggleBackground">
            Háttér változtatás
          </button>
          <button class="dropdown-item" @click="logout">Kijelentkezés</button>
        </div>
      </div>
    </div>

    <div class="vonal"></div>
    <div class="editor-wrapper">
      <MdEditor
        v-model="contents"
        language="en-US"
        v-on:upload-img="imgupload"
        class="custom-editor"
      />
    </div>
  </div>
</template>
<script setup lang="ts">
import { MdEditor } from "md-editor-v3";
import "md-editor-v3/lib/style.css";
import { ref } from "vue";

const contents = ref("# Hello World");
const imgupload = (e) => {
  console.debug("Uploaded img" + e);
};

const backgrounds = ["imgs/day.jpg", "imgs/night.jpg"];
const currentBackground = ref(backgrounds[0]);

const toggleBackground = () => {
  currentBackground.value =
    currentBackground.value === backgrounds[0]
      ? backgrounds[1]
      : backgrounds[0];
};

const dropdownVisible = ref(false);
const toggleDropdown = () => {
  dropdownVisible.value = !dropdownVisible.value;
};

const logout = () => {
  console.log("Kijelentkezés");

};
</script>

<style scoped>
.vonal {
  width: 90dvw; 
  max-width: 1700px;
  height: 2px; 
  background-color: #000;
  margin: 0 auto; 
}
.editor-container {
  position: relative;
  width: 100%;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  background-repeat: no-repeat;
  background-size: cover;
  transition: background 0.5s ease;
}

.nav-bar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  padding: 10px 20px;
  color: rgb(0, 0, 0);
  z-index: 10;
  backdrop-filter: blur(10px);
}

.back-button {
  background: none;
  border: none;
  color: rgb(0, 0, 0);
  font-size: 20px;
  cursor: pointer;
  text-shadow: 0 1px 3px rgba(0, 0, 0, 0.5); 
}

.user-button {
  background: none;
  border: none;
  color: rgb(0, 0, 0);
  font-size: 20px;
  cursor: pointer;
  text-shadow: 0 1px 3px rgba(0, 0, 0, 0.5); 
}

.user-button:hover {
  color: #007bff; 
  transform: scale(1.1);
}

.title {
  font-size: 20px;
  font-weight: bold;
  text-shadow: 0 1px 3px rgba(0, 0, 0, 0.5); /* Szöveg árnyékolása */
}

.user-dropdown {
  position: relative;
}

.dropdown-menu {
  position: absolute;
  top: 30px;
  right: 0;
  background: white;
  border: 1px solid #ccc;
  border-radius: 5px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  z-index: 100;
}

.dropdown-item {
  padding: 5px 20px;
  cursor: pointer;
  font-size: 13px;
  color: #0a0a0a;
  background: rgb(252, 251, 251);
  border: none;
  text-align: center;
  width: 100%;
}

.dropdown-item:hover {
  background: #5171ffe5;
}

.editor-wrapper {
  width: 90%;
  height: 80%;
  display: flex;
  flex-direction: column;
  align-items: center;
  position: relative;
  margin-top: 20px; 
}

.custom-editor {
  width: 100%;
  height: 100%;
  background: rgba(255, 255, 255, 0.1); 
  backdrop-filter: blur(10px); 
  border-radius: 15px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
  overflow: hidden;
  display: flex;
  flex-direction: column;
}
</style>
