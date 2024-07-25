<template>
  <div class="home">

    <h2> {{ appTitle }} </h2>

    <h2>{{ dataCount.title }} :</h2>

    <div>
      
      <button class="btn minus" @click="decreaseCounter(2)"> -- </button>
      <button class="btn minus" @click="decreaseCounter(1)"> - </button>
      <span class="counter"> {{ dataCount.count }} </span>
      <button class="btn plus" @click="increaseCounter(1)"> + </button>
      <button class="btn plus" @click="increaseCounter(2)"> ++ </button>
    </div>

    <div>
      <label for="">Edit counter title</label>
      <input type="text" v-model="dataCount.title" />
    </div>

  </div>
</template>

<script setup>
import { reactive } from "vue";

const appTitle = "the application title"

const dataCount = reactive({
  count: 0,
  title: "my counter title",
});

const increaseCounter = (amount) => {
  dataCount.count += amount;
};


const decreaseCounter = (amount) => {
  dataCount.count -= amount;
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