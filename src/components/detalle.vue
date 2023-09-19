<script setup>
import axios from 'axios'
import { ref } from 'vue';

let imagen = ref([])
let numero = ref("")
let nombre = ref("")
let tipo = ref([])
let altura = ref("")
let peso =  ref("")
let hp = ref("")
let attack = ref("")
let defense = ref("")
let special_attack = ref("")
let special_defense = ref("")
let speed = ref("")




async function obtenerUrlPokemon() {
  // let r = await axios.get("https://pokeapi.co/api/v2/pokemon?limit=50&offset=0")

  let r = await axios.get("https://pokeapi.co/api/v2/pokemon/34/")
  imagen.value = r.data.sprites.other['official-artwork'].front_default
  numero.value = r.data.id
  nombre.value = r.data.name
  tipo.value = [] 
  for (let i = 0; i < r.data.types.length; i++) {
    tipo.value.push(r.data.types[i].type);
  }
  altura.value = r.data.height
  peso.value = r.data.weight
  for (let j = 0; j < r.data.stats.length; j++) {
    hp.value = r.data.stats[0].base_stat
    attack.value = r.data.stats[1].base_stat
    defense.value = r.data.stats[2].base_stat
    special_attack.value = r.data.stats[3].base_stat
    special_defense.value = r.data.stats[4].base_stat
    speed.value = r.data.stats[5].base_stat
  }
}
</script>

<template>
  <div>
    <button @click="obtenerUrlPokemon()">Peticion</button>
    <img :src="imagen" alt="">
    <p>Numero:   {{ numero }} </p>
    <p>Nombre:   {{ nombre }}</p>
    <p>Tipo:</p>
    <div  v-for="(item,index) in tipo" :key="index">
      <p>{{ item.name }}</p>
    </div>
    <p>Altura:  {{ altura }}</p>
    <p>Peso:  {{ peso }} </p>
    <p>Stats</p>
    <p>Hp: {{ hp }}</p>
    <p>Attack: {{ attack }}</p>
    <p>Defense: {{ defense }}</p>
    <p>Special Attack: {{ special_attack }}</p>
    <p>Special Defense: {{ special_defense }}</p>
    <p>Speed: {{ speed }}</p>
  </div>
</template>

<style scoped>

</style>