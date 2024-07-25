<template>
  <div class="home">
    <h2>{{ counterTitle }} :</h2>

    <div>
      <button class="btn minus" @click="decreaseCounter">-</button>
      <span class="counter"> {{ counter }} </span>
      <button class="btn plus" @click="increaseCounter">+</button>
    </div>

    <div>
      <input type="text" v-model="counterTitle" />
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const counter = ref(0),
  counterTitle = ref("Counter title");

const increaseCounter = () => {
  counter.value++;
};

const decreaseCounter = () => {
  if (counter.value > 0) counter.value--;
};
</script>




<style scoped>
.home {
  text-align: center;
  margin: 40px;
}

.btn {
  font-size: 30px;
  padding: 10px;
  margin: 20px;
}

.counter {
  font-size: 20px;
}
</style>