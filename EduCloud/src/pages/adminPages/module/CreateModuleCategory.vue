<script setup>

import {ref} from "vue";

const inputValues = ref(['','',''])

const inputValuesSum = ref("")
</script>

<template>
  <section class="w-full h-full">
    <div class="flex w-full justify-center items-center text-2xl h-[7dvh] font-bold border-b-[1px] border-b-gray-800">
      <span>Modul kategória létrehozása</span>
    </div>

    <div class="flex flex-col justify-center align-middle mt-[23vh] w-full">
      <div class="flex gap-44 justify-center align-middle py-8">
        <div class="relative">
          <input
              v-model="inputValues[0]"
              type="text"
              placeholder="Modul címe"
              class="w-[12dvw] py-2 px-2 text-gray-800 border-none outline-none focus:ring-0 text-center bg-transparent"
          />
          <hr class="absolute w-full h-[3px] bg-black shadow-2xl top-full" />
        </div>

        <div class="relative">
          <input
              v-model="inputValues[1]"
              type="text"
              placeholder="Modul címe"
              class="w-[12dvw] py-2 px-2 text-gray-800 border-none outline-none focus:ring-0 text-center bg-transparent"
          />
          <hr class="absolute w-full h-[3px] bg-black shadow-2xl top-full" />
        </div>

        <div class="relative">
          <input
              v-model="inputValues[2]"
              type="text"
              placeholder="Modul címe"
              class="w-[12dvw] py-2 px-2 text-gray-800 border-none outline-none focus:ring-0 text-center bg-transparent"
          />
          <hr class="absolute w-full h-[3px] bg-black shadow-2xl top-full" />
        </div>


      </div>


        <!-- Grade Select -->


      <!-- Clear Button -->
      <div class="w-full flex justify-center align-middle">
        <button
            @click="()=>{inputValues = ['','','']}"
            class="max-w-[14dvw] mt-4 py-2 px-4 bg-gray-600 text-white font-semibold rounded-lg hover:bg-gray-800 active:bg-gray-600"
        >
          Válaszok törlése
        </button>
      </div>

      <!-- some ass function to display them, works at least -->
      <div class="flex flex-col items-center py-8" >
        <button
            @click="()=>inputValuesSum = `${inputValues[0]}, ${inputValues[1]}, ${inputValues[2]}`"
            class="rounded-md max-w-[10dvw] py-1 px-12 border border-gray-300 text-center bg-gray-100 hover:bg-gray-300 active:bg-gray-100"
        >Mentés</button>
        <p>{{inputValuesSum}}</p>
      </div>

    </div>
  </section>

</template>