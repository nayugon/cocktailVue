<script setup>
import { ref } from 'vue'

let bebida=ref("Rum");
const cambiarVodka = () => bebida.value="Vodka"
const cambiarRon = () => bebida.value="Rum"


let array = ref(null);
const url = "https://www.thecocktaildb.com/api/json/v1/1/filter.php?i=Rum"

const api= async () => {
  const respuesta = await fetch(url)
    .then((resp) => resp.json())
    .then((resp) => resp.drinks)
  array.value=respuesta;
}

api();  

</script>

<template>
<div>{{bebida}}</div>

<button @click="cambiarVodka">vodka</button>
<button @click="cambiarRon">Ron</button>

<div v-if="array!=null">
  <div v-for="dato in array"><img :src=dato.strDrinkThumb alt="" width="150px" height="150px"><br>{{ dato.strDrink }}</div>
</div>
<p v-else>cargando...</p>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
div {
  border-color: blue;
  border-style: solid;
  padding: 1px;
}
</style>
