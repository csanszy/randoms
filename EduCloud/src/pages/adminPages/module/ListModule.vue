<script setup lang="ts">

import {computed, ref} from "vue";

  const modules = ref('')


  modules.value = [
   { id: 1, name: 'Express alapok', description: 'almavagyok', grade: '13', createdAt: '2024.06.25 12:00:00', categoryName: 'Backend', professionName: 'Szoftverfejleszto' },
   { id: 2, name: 'Java alapok', description: 'almavagyok', grade: '13', createdAt: '2024.06.25 12:00:00', categoryName: 'Backend', professionName: 'Szoftverfejleszto' },
   { id: 3, name: 'C# alapok', description: 'almavagyok', grade: '13', createdAt: '2024.06.25 12:00:00', categoryName: 'Backend', professionName: 'Szoftverfejleszto' },
   { id: 4, name: 'HTML alapok', description: 'almavagyok', grade: '13', createdAt: '2024.06.25 12:00:00', categoryName: 'Backend', professionName: 'Szoftverfejleszto' },
   { id: 5, name: 'CSS alapok', description: 'almavagyok', grade: '13', createdAt: '2024.06.25 12:00:00', categoryName: 'Backend', professionName: 'Szoftverfejleszto' },
   { id: 6, name: 'PHP alapok', description: 'almavagyok', grade: '13', createdAt: '2024.06.25 12:00:00', categoryName: 'Backend', professionName: 'Szoftverfejleszto' },
   { id: 7, name: 'Random alapok', description: 'almavagyok', grade: '13', createdAt: '2024.06.25 12:00:00', categoryName: 'Backend', professionName: 'Szoftverfejleszto' },
 ];

const nameSearchQuery = ref('');

  const filteredModulesByName = computed(() => {
    return modules.value.filter(module =>
        module.name.toLowerCase().includes(nameSearchQuery.value.toLowerCase())
    );
  });

  //delete function
  function deleteModule(id: number) {
    modules.value.map((value:any, index)=>{
      if(id == value.id) {
        modules.value.splice(index, 1)
      }
    })
  }



  const tableCols = ['ID','Name','Grade','Description','Category','Profession','CreatdAt','Edit','Delete'];

</script>

<template>

  <section class="w-full h-full flex flex-col  items-center">

    <div class="flex w-full justify-center items-center text-2xl h-[7dvh] font-bold border-b-[1px] border-b-gray-800">
      <span>Modulok</span>
    </div>

    <div class="mt-8 flex-nowrap flex flex-col items-center">

      <div v-if="modules.length <= 0" >
        <h1 class="form-title">Nincsenek elérhető modulok</h1>
      </div>
      <div v-if="modules.length > 0" class="my-8 relative">
        <input v-model="nameSearchQuery" type="text" placeholder="Keresés" class="w-[10dvw] bg-transparent text-center focus:outline-none" />🔍
        <hr class="absolute w-full h-[2px] bg-black shadow-2xl top-full" />
      </div>

      <div v-if="modules.length > 0" class=" border rounded-md bg-gray-400">
        <table class="min-w-[60dvw] text-center">
          <thead>
          <tr class="">
            <th v-for="content in tableCols" :key="content">{{content}}</th>
          </tr>
          </thead>
          <tbody>
          <tr v-for="(module, index) in filteredModulesByName" :key="index" class="odd:bg-gray-200 even:bg-gray-300">
            <td>{{ module.id }}</td>
            <td>{{ module.name }}</td>
            <td>{{ module.grade }}</td>
            <td>{{ module.description }}</td>
            <td>{{ module.categoryName }}</td>
            <td>{{ module.professionName }}</td>
            <td>{{ module.createdAt }}</td>
            <td>
              <button @click="editModule(module.id)" class="delete-button">
                ✎
              </button>
            </td>
            <td>
              <button @click="deleteModule(module.id)" class="delete-button">
                Törlés
              </button>
            </td>
          </tr>
          </tbody>
        </table>
      </div>
    </div>
  </section>

</template>
