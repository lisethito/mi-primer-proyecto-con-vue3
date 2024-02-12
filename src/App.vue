<template>
  <div class="container text-center">
    <h1>Agregar números</h1>
    <div class="btn-group">
      <button @click="increment" class="btn btn-success">Aumentar</button>
      <button @click="decrement" class="btn btn-secondary">Disminuir</button>
      <button @click="reset" class="btn btn-danger">Resetear</button>
      <button @click="add" :disabled="bloquearBtnAdd" class="btn btn-primary">
        Agregar
      </button>
    </div>

    <h2 :class="classCounter">{{ counter }}</h2>

    <ul class="list-group mt-4">
      <li
        class="list-group-item"
        v-for="(num, index) in arrayFavoritos"
        :key="index"
      >
        {{ num }}
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";
const counter = ref(0);
const arrayFavoritos = ref([]);
const increment = () => {
  counter.value++;
};
const decrement = () => {
  counter.value--;
};
const reset = () => {
  counter.value = 0;
};
const add = () => {
  arrayFavoritos.value.push(counter.value);
};
const bloquearBtnAdd = computed(() => {
  const numSearch = arrayFavoritos.value.find((num) => num === counter.value);
  console.log(numSearch);
  if (numSearch === 0) return true;
  return numSearch ? true : false;
});

const classCounter = computed(() => {
  if (counter.value === 0) {
    return "zero";
  }
  if (counter.value > 0) {
    return "positive";
  }
  if (counter.value < 0) {
    return "negative";
  }
});
</script>

<style>
.positive {
  color: green;
}
.negative {
  color: red;
}
.zero {
  color: peru;
}
</style>
