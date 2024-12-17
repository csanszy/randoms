<script setup lang="ts">

import {computed, ref} from "vue";
import {useRoute} from "vue-router";
import ListShow from "./list/ListShow.vue";

const assignments = ref('')


assignments.value = [
  {
    id:1,
    name: "Express Basics",
    category: "Express alapok",
    grade: "Beginner",
    profession: "Web Developer",
    items: [
      { id: 1, name: "Introduction to Express", fileName: "intro_express.md" },
      { id: 2, name: "Express Routing", fileName: "express_routing.md" },
      { id: 3, name: "Middleware Basics", fileName: "middleware_basics.md" },
    ],
  },
  {
    id:2,
    name: "Java Basics",
    category: "Java alapok",
    grade: "Intermediate",
    profession: "Software Engineer",
    items: [
      { id: 4, name: "Java Basics", fileName: "java_basics.md" },
      { id: 5, name: "OOP in Java", fileName: "oop_java.md" },
      { id: 6, name: "Exception Handling", fileName: "exception_handling.md" },
    ],
  },
  {
    id:3,
    name: "C# Basics",
    category: "C# alapok",
    grade: "Intermediate",
    profession: "Software Developer",
    items: [
      { id: 7, name: "C# Syntax", fileName: "csharp_syntax.md" },
      { id: 8, name: "Data Types in C#", fileName: "data_types_csharp.md" },
      { id: 9, name: "LINQ Basics", fileName: "linq_basics.md" },
    ],
  },
  {
    id:4,
    name: "HTML Basics",
    category: "HTML alapok",
    grade: "Beginner",
    profession: "Frontend Developer",
    items: [
      { id: 10, name: "HTML Structure", fileName: "html_structure.md" },
      { id: 11, name: "Forms and Inputs", fileName: "forms_inputs.md" },
      { id: 12, name: "HTML5 Features", fileName: "html5_features.md" },
    ],
  },
  {
    id:5,
    name: "CSS Basics",
    category: "CSS alapok",
    grade: "Beginner",
    profession: "Frontend Developer",
    items: [
      { id: 13, name: "CSS Selectors", fileName: "css_selectors.md" },
      { id: 14, name: "Flexbox Basics", fileName: "flexbox_basics.md" },
      { id: 15, name: "Grid Layout", fileName: "grid_layout.md" },
    ],
  },
  {
    id:6,
    name: "PHP Basics",
    category: "PHP alapok",
    grade: "Intermediate",
    profession: "Backend Developer",
    items: [
      { id: 16, name: "PHP Syntax", fileName: "php_syntax.md" },
      { id: 17, name: "Working with Arrays", fileName: "arrays_php.md" },
      { id: 18, name: "Intro to PDO", fileName: "intro_pdo.md" },
    ],
  },
  {
    id:7,
    name: "Random Basics",
    category: "Random alapok",
    grade: "Advanced",
    profession: "Generalist",
    items: [
      { id: 19, name: "Random Topic 1", fileName: "random_topic_1.md" },
      { id: 20, name: "Random Topic 2", fileName: "random_topic_2.md" },
      { id: 21, name: "Random Topic 3", fileName: "random_topic_3.md" },
    ],
  },
];
const nameSearchQuery = ref('');

const filteredAssignmentsByName = computed(() => {
  return assignments.value.filter(assignment =>
      assignment.name.toLowerCase().includes(nameSearchQuery.value.toLowerCase())
  );
});

//delete function
function deleteAssignment(id: number) {
  assignments.value.map((value:any, index)=>{
    if(id == value.id) {
      assignments.value.splice(index, 1)
    }
  })
}
// Define a reactive property to store the selected item
const selectedItem = ref(null);

// Method to handle the click event and store the selected item
const handleItemClick = (item) => {
  selectedItem.value = item;  // Set the clicked item to the reactive property
};



const tableCols = ['Name','Grade','Category','Profession','Edit','Delete'];

</script>

<template>

  <section class="w-full h-full flex flex-col  items-center">

    <div class="flex w-full justify-center items-center text-2xl h-[7dvh] font-bold border-b-[1px] border-b-gray-800">
      <span>Modulok</span>
    </div>

    <div class="mt-8 flex-nowrap flex flex-col items-center">

      <div class="h-full w-full flex justify-center items-center">
        <p>Válasszon egy modult amiben keresni szeretne.</p>
      </div>

      <router-view/>

      <div v-if="assignments.length <= 0" >
        <h1 class="form-title">Nincsenek elérhető modulok</h1>
      </div>
      <div v-if="assignments.length > 0" class="my-8 relative">
        <input v-model="nameSearchQuery" type="text" placeholder="Keresés" class="w-[10dvw] bg-transparent text-center focus:outline-none" />🔍
        <hr class="absolute w-full h-[2px] bg-black shadow-2xl top-full" />
      </div>

      <div v-if="assignments.length > 0" class=" border rounded-md bg-gray-400">
        <table class="min-w-[60dvw] text-center">
          <thead>
          <tr class="">
            <th v-for="content in tableCols" :key="content" class="px-4">{{content}}</th>
          </tr>
          </thead>
          <tbody>
          <tr v-for="(assignment, index) in filteredAssignmentsByName" :key="index" class="odd:bg-gray-200 even:bg-gray-300">
            <td>
              <button @click="handleItemClick(assignment)" class="text-gray-700 hover:text-gray-500 active:text-gray-700">{{ assignment.name }}</button>
            </td>
            <td>
              {{ assignment.grade }}
            </td>
            <td>
              {{ assignment.category }}
            </td>
            <td>
              {{ assignment.profession }}
            </td>
            <td>
              <button @click="editAssignment(assignment.id)" class="delete-button">
                ✎
              </button>
            </td>
            <td>
              <button @click="deleteAssignment(assignment.id)" class="delete-button">
                Törlés
              </button>
            </td>
          </tr>
          </tbody>
        </table>
      </div>
      <div class="h-full w-full flex justify-center items-center">
        <ListShow :selectedItem="selectedItem" />
      </div>
    </div>
  </section>

</template>
