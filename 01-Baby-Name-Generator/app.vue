<script setup lang="ts">
import { Gender, Popularity, Length, names } from "@/data"

interface OptionsState {
  gender: Gender;
  popularity: Popularity;
  length: Length
}

const options = reactive<OptionsState>({
  gender: Gender.BOY,
  popularity: Popularity.UNIQUE,
  length: Length.ALL
})

const selectedNames = ref<string[]>([])

const computeSelectedNames = () => {
  const filteredNames = names.filter(name => name.gender === options.gender)
    .filter(name => name.popularity === options.popularity)
    .filter(name => {
      if(options.length === Length.ALL) return true
      else return name.length === options.length
    })
    
  selectedNames.value = filteredNames.map(name => name.name)
}



const optionsArray = [
  {
    title: "1) Choose a gender",
    category: "gender",
    buttons: [Gender.GIRL, Gender.BOY, Gender.UNISEX]
  },
  {
    title: "2) Choose name's popularity",
    category: "popularity",
    buttons: [Popularity.TRENDY, Popularity.UNIQUE]
  },
  {
    title: "3) Choose name's length",
    category: "length",
    buttons: [Length.ALL, Length.LONG, Length.SHORT]
  }
]

const removeName = (index: number) => {
  const filteredNames = [...selectedNames.value]
  filteredNames.splice(index, 1)
  selectedNames.value = filteredNames
}

</script>

<template>
  <div class="container">
    <h1>Baby Name Generator</h1>
    <p>Choose your options anc click "Find Names" button below</p>
    <div class="options-container">

      <!-- options -->
      <Option  v-for="option in optionsArray" :key="option.title" :option="option" :options="options"/>

      <!-- Find -->
      <button @click="computeSelectedNames" class="primary">Find Names</button>
    </div>

    <div class="cards-container">
      <CardName v-for="(name, index) in selectedNames" :key="name" :name="name" :index="index" @remove="removeName(index)"/>
    </div>

  </div>
</template>

<style scoped>
.container {
  font-family: Arial, Helvetica, sans-serif;
  color: rgb(27, 60, 138);
  max-width: 50rem;
  margin: 0 auto;
  text-align: center;


  /* border: 1px solid red; */
}

h1 {
  font-size: 3rem;
}

.options-container {
  background-color: rgb(255, 238, 236);
  border-radius: 2rem;
  padding: 2rem;
  width: 95%;
  margin: 0 auto;
  margin-top: 2rem;
  position: relative;

  /* border: 1px solid red; */
}

.primary {
  background-color: rgb(249, 87, 89);
  color: white;
  border-radius: 6.5rem;
  border: none;
  padding: 0.75rem 4rem;
  font-size: 1rem;
  margin-top: 1rem;
  cursor: pointer;
}

.primary:hover {
  background-color: rgb(221, 90, 162);
}

.cards-container{
  display: flex;
  margin-top: 3rem;
  flex-wrap: wrap;
}


</style>
