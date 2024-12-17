
<script setup lang="ts">
import {useRouter} from "vue-router";

const router = useRouter()

const goBack = () => {
  router.go(-1)
}
</script>

<template>
  <div class="flex flex-col justify-center items-center h-screen text-center bg-gradient-to-r from-blue-500 to-purple-500">
    <h1 class="text-6xl">404</h1>
    <p class="text-xl">Page not found</p>
    <button @click="goBack"
            class="font-bold py-2 px-4">
      Go pervious</button>
    <router-link to="/">
      <button class="font-bold py-2 px-4">
        Go home
      </button>

    </router-link>
  </div>
</template>