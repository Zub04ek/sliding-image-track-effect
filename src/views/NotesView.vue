<template>
  <div>
    <main class="w-screen h-screen">
      <button
        @click="router.back()"
        class="fixed z-[9] top-[37px] left-[40px] text-[16px] text-white hover:text-[#00bd7e] leading-5 overflow-hidden transition-colors duration-300"
      >
        Back
      </button>
      <div v-if="showModal" class="overlay absolute w-full h-full bg-[rgba(51,51,51,0.8)] z-10 flex items-center justify-center">
        <div class="modal w-[750px] bg-white relative p-[30px] rounded-[10px] flex flex-col">
            <textarea v-model.trim="newNote" name="note" id="note" cols="30" rows="10" class="text-black border border-blue-800"></textarea>
            <p v-if="errorMessage" class="text-red-900">{{ errorMessage }}</p>
            <button @click="addNote" type="button" class="py-[10px] px-[20px] w-full rounded-full bg-indigo-600 text-[20px] mt-[15px]">Add Note</button>
            <button @click="showModal = false" type="button" class="py-[10px] px-[20px] w-full rounded-full bg-red-800 text-[20px] mt-[7px]">Close</button>
        </div>
      </div>
      <div class="container max-w-[1000px] p-[10px] mx-auto my-0">
        <header class="flex justify-between items-center">
          <h1 class="font-bold mb-[25px] text-[75px]">Notes</h1>
          <button @click="showModal = true" type="button" class="p-[10px] w-[50px] h-[50px] rounded-full bg-white text-[20px] text-center text-black font-bold">+</button>
        </header>
        <ul class="card-container flex flex-wrap gap-5 text-black">
          <li v-for="{id, text, date, bcgColor} in notes" :key="id" :style="{'background-color': bcgColor}" class="card w-[225px] h-[225px] p-[10px] rounded-[15px] flex flex-col justify-between">
            <p class="main-text ">{{ text }}</p>
            <p class="date text-[12.5px] font-bold">{{ date.toLocaleDateString("en-US") }}</p>
          </li>
        </ul>
      </div>
    </main>
  </div>
</template>

<script setup lang="js">
import { ref } from 'vue'
import router from '../router'

const showModal = ref(false)
const newNote = ref("")
const notes = ref([])
const errorMessage = ref("")

function getRandomColor() {
  return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
}

const addNote = () => {
  if (newNote.value.length < 10) {
    return errorMessage.value = "Note needs to be 10 characters or more"
  }
     notes.value.push({
        id: Math.floor(Math.random() * 1000000),
        text: newNote.value,
        date: new Date(),
        bcgColor: getRandomColor()
    })
    showModal.value = false;
    newNote.value = "";
    errorMessage.value = "";
}
</script>

<style scoped></style>
