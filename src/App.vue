<script setup>
import { ref } from "vue";
import style from "./cardStyle.module.css";
import Card from "./components/Card/Card.vue";

const cars = ref([
  { car: "Toyota" },
  { car: "BMW" },
  { car: "Mercedes" },
  { car: "Lamborghini" },
  { car: "Tokada" },
]);
const input = ref("");
function getIsVisible(car) {
  return car.toLowerCase().includes(input.value.toLowerCase());
}

const isOpen = ref(false);
</script>


<template>
  <input v-model="input" />
  <template v-for="({ car }, i) in cars">
    <div :class="style.car" v-if="getIsVisible(car)">
      <h1>{{ car }}</h1>
      <Card v-slot="{ quantity }">
        <h2>Click to purchase </h2>
        <p>Quantity in stock {{ quantity }}</p>
      </Card>
    </div>
  </template>
</template>
<style scoped>
</style>
