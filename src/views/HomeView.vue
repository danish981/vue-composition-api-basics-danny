<template>
  <div class="home">
    <h2>{{ dataCount.title }} :</h2>

    <div>
      <button class="btn minus" @click="decreaseCounter"> - </button>
      <span class="counter"> {{ dataCount.count }} </span>
      <button class="btn plus" @click="increaseCounter"> + </button>
    </div>

    <div>
      <input type="text" v-model="dataCount.title" />
    </div>
  </div>
</template>

<script setup>
import { reactive } from "vue";

const dataCount = reactive({
  count: 0,
  title: "my counter title",
});

const increaseCounter = () => {
  dataCount.count++;
};

const decreaseCounter = () => {
  dataCount.count--;
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