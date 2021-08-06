<template>
  <div id='olympics'>Olympics {{ year }}</div>
  <button @click="decreaseYear()">Previous Olympics</button>
  <button @click="currentYear()">Current Olympics</button>
  <button @click="increaseYear()">Next Olympics</button>
  <p>{{ obj.name }}</p>
  <ul>
    <p>Capacity: {{ capacity }}</p>
    <li v-for="(country, index) in countries" :key="index">
      {{ country }}
    </li>
  </ul>
  <br />
  <br />
  <p>Spaces Left: {{ spacesLeft }} out of {{ capacity }}</p>
  <button @click="increaseCapacity()">increase Capacity</button>
</template>

<script>
import { computed, ref } from 'vue'

export default {
  components: {
  },
  setup() {
    const year = ref(2020)
    const obj = ref({ name: 'Tiago', age: 35 })
    setTimeout(() => {
      obj.value.name = 'Diego'
    }, 2000)

    const capacity = ref(3)
    const countries = ref(['BR', 'DK', 'FR', 'RU'])
    const spacesLeft = computed(() => capacity.value - countries.value.length)

    function increaseCapacity() {
      capacity.value += 1
    }

    function increaseYear() {
      year.value += 4
    }
    function decreaseYear() {
      year.value -= 4
    }
    function currentYear() {
      year.value = 2020
    }
    return {
      year,
      countries,
      capacity,
      obj,
      spacesLeft,
      increaseCapacity,
      increaseYear,
      decreaseYear,
      currentYear,
    }
  },
}
</script>
