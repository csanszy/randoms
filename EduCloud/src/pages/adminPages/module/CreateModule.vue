
<style>
textarea::placeholder {
  height: 2rem;
  padding-top: 4rem;
}
textarea{
  height: 2rem;
}
</style>

<template>

  <section class="w-full h-full">
    <div class="flex w-full justify-center items-center text-2xl h-[7dvh] font-bold border-b-[1px] border-b-gray-800">
      <span>Modul létrehozása</span>
    </div>

    <div class="flex flex-col justify-center align-middle mt-[23vh] w-full">
      <div class="flex gap-44 justify-center align-middle py-8">
        <div class="relative">
          <input
              type="text"
              placeholder="Modul címe"
              class="w-[12dvw] py-2 px-2 text-gray-800 border-none outline-none focus:ring-0 text-center bg-transparent"
          />
          <hr class="absolute w-full h-[3px] bg-black shadow-2xl top-full" />
        </div>

        <div class="relative">
          <!-- textarea because if the description  is too long it needs to be split into separate lines-->
          <textarea
              placeholder="Modul leírása"
              class="w-[12dvw] px-2 py-2 text-gray-800 resize-none border-none outline-none text-center overflow-auto bg-transparent"
          />
          <hr class="absolute w-full h-[3px] bg-black shadow-2xl top-full" />
        </div>
      </div>

      <div class="flex flex-row justify-center align-middle gap-44 w-full py-4">
        <!-- Grade Select -->
        <div class="min-w-[14dvw]">

          <select
              id="grade"
              v-model="selectedGrade"
              @change="filterBasedOnSelection('grade')"
              class="block w-full mt-2 p-2 border border-gray-300 bg-gray-100 hover:bg-gray-200 focus:bg-gray-100 active:bg-gray-300 rounded-lg text-center"
          >
            <!-- before anyone tries, you cannot center options, I tried for 30 minutes straight -->
            <option value="" disabled hidden>Osztály</option>
            <option value="" disabled >Válasszon egy osztályt</option>

            <option v-for="grade in filteredGrades" :key="grade" :value="grade">{{ grade }}</option>
          </select>
        </div>

        <!-- Category Select -->
        <div class="min-w-[14dvw]">
          <select
              id="category"
              v-model="selectedCategory"
              @change="filterBasedOnSelection('category')"
              class="block w-full mt-2 p-2 border border-gray-300 bg-gray-100 hover:bg-gray-200 focus:bg-gray-100 active:bg-gray-300 rounded-lg text-center"
          >
            <option value="" disabled hidden>Kategória</option>
            <option value="" disabled >Válasszon egy kategóriát</option>
            <option v-for="category in filteredCategories" :key="category" :value="category">{{ category }}</option>
          </select>
        </div>

        <!-- Profession Select -->
        <div class="min-w-[14dvw]">
          <select
              id="profession"
              v-model="selectedProfession"
              @change="filterBasedOnSelection('profession')"
              class="block w-full mt-2 p-2 border border-gray-300 bg-gray-100 hover:bg-gray-200 focus:bg-gray-100 active:bg-gray-300 rounded-lg text-center"
          >
            <option value="" disabled hidden>Szakma</option>
            <option value="" disabled >Válasszon egy szakmát</option>
            <option v-for="profession in filteredProfessions" :key="profession" :value="profession">{{ profession }}</option>
          </select>
        </div>
      </div>

      <!-- Clear Button -->
      <div class="w-full flex justify-center align-middle">
        <button
            @click="clearSelections"
            class="max-w-[14dvw] mt-4 py-2 px-4 bg-gray-600 text-white font-semibold rounded-lg hover:bg-gray-800 active:bg-gray-600"
        >
          Választások törlése
        </button>
      </div>

      <div class="flex gap-44 justify-center align-middle py-8 ">
        <input class="border-b text-center focus:outline-none" placeholder="Modul címe" type="file">
        <button class="rounded-md py-1 border border-gray-300  px-12 text-center bg-gray-100 hover:bg-gray-300 active:bg-gray-100" >Fájl szerkesztése</button>
      </div>

      <div class="flex gap-44  justify-center align-middle py-8" >
        <button
              class="rounded-md py-1 px-12 border border-gray-300 text-center bg-gray-100 hover:bg-gray-300 active:bg-gray-100"
        >Mentés</button>
      </div>

    </div>
  </section>

</template>

<script setup>
import { ref, computed } from 'vue'

// Sample expanded data structure
const grades = ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H']
const categories = {
  A: ['Math', 'Science'],
  B: ['History', 'Geography', "Math"],
  C: ['Literature', 'Arts'],
  D: ['Biology', 'Chemistry'],
  E: ['Physics', 'Astronomy'],
  F: ['Philosophy', 'Sociology'],
  G: ['Law', 'Politics'],
  H: ['Economics', 'Psychology']
}
const professions = {
  A: ['Engineer', 'Scientist'],
  B: ['Teacher', 'Historian'],
  C: ['Writer', 'Artist'],
  D: ['Biologist', 'Chemist'],
  E: ['Physicist', 'Astronomer'],
  F: ['Philosopher', 'Sociologist'],
  G: ['Lawyer', 'Politician'],
  H: ['Economist', 'Psychologist']
}

// Reverse mapping to easily find which grades each category or profession is associated with
const categoryToGrades = {
  Math: ['A', 'B'],
  Science: ['A', 'D'],
  History: ['B'],
  Geography: ['B', 'C'],
  Literature: ['C'],
  Arts: ['C', 'D'],
  Biology: ['D', 'E'],
  Chemistry: ['D', 'E'],
  Physics: ['E', 'F'],
  Astronomy: ['E'],
  Philosophy: ['F'],
  Sociology: ['F'],
  Law: ['G'],
  Politics: ['G'],
  Economics: ['H'],
  Psychology: ['H']
}

const professionToGrades = {
  Engineer: ['A', 'B'],
  Scientist: ['A'],
  Teacher: ['B'],
  Historian: ['B', 'C'],
  Writer: ['C', 'D'],
  Artist: ['C', 'D'],
  Biologist: ['D', 'E'],
  Chemist: ['D', 'E'],
  Physicist: ['E'],
  Astronomer: ['E'],
  Philosopher: ['F'],
  Sociologist: ['F'],
  Lawyer: ['G'],
  Politician: ['G'],
  Economist: ['H'],
  Psychologist: ['H']
}

// Reactive state for selections
const selectedGrade = ref('')
const selectedCategory = ref('')
const selectedProfession = ref('')

// Filtered categories and professions based on selected grade
const filteredCategories = computed(() => {
  if (!selectedGrade.value) return Object.values(categories).flat()
  return categories[selectedGrade.value] || []
})

const filteredProfessions = computed(() => {
  if (!selectedGrade.value) return Object.values(professions).flat()
  return professions[selectedGrade.value] || []
})

// Filtered grades based on selected category and profession
const filteredGrades = computed(() => {
  let validGrades = grades
  if (selectedCategory.value) {
    validGrades = validGrades.filter(grade => categoryToGrades[selectedCategory.value]?.includes(grade))
  }
  if (selectedProfession.value) {
    validGrades = validGrades.filter(grade => professionToGrades[selectedProfession.value]?.includes(grade))
  }
  return validGrades
})

// Dynamically filter grade, category, and profession based on the current selection
const filterBasedOnSelection = (field) => {
  if (field === 'grade') {
    // If grade is selected, filter category and profession
    if (selectedGrade.value) {
      if (!filteredCategories.value.includes(selectedCategory.value)) {
        selectedCategory.value = ''
      }
      if (!filteredProfessions.value.includes(selectedProfession.value)) {
        selectedProfession.value = ''
      }
    }
  } else if (field === 'category') {
    // If category is selected, filter grade and profession
    if (selectedCategory.value) {
      selectedGrade.value = Object.keys(categories).find(grade =>
          categories[grade].includes(selectedCategory.value)
      ) || ''
      if (!filteredProfessions.value.includes(selectedProfession.value)) {
        selectedProfession.value = ''
      }
    }
  } else if (field === 'profession') {
    // If profession is selected, filter grade and category
    if (selectedProfession.value) {
      selectedGrade.value = Object.keys(professions).find(grade =>
          professions[grade].includes(selectedProfession.value)
      ) || ''
      if (!filteredCategories.value.includes(selectedCategory.value)) {
        selectedCategory.value = ''
      }
    }
  }
}

// Clear all selections
const clearSelections = () => {
  selectedGrade.value = ''
  selectedCategory.value = ''
  selectedProfession.value = ''
}
</script>

<style scoped>
/* Tailwind is already sufficient for basic styling */
</style>
