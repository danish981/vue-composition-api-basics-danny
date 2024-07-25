<template>
  <div class="home">
    <header>
      <h1>{{ appTitle }}</h1>
    </header>

    <section class="counter-section">
      <h2>{{ dataCount.title }} :</h2>
      <div class="counter-controls">
        <button class="btn btn-minus" @click="decreaseCounter(2)"> -- </button>
        <button class="btn btn-minus" @click="decreaseCounter(1)"> - </button>
        <span class="counter">{{ dataCount.count }}</span>
        <button class="btn btn-plus" @click="increaseCounter(1)"> + </button>
        <button class="btn btn-plus" @click="increaseCounter(2)"> ++ </button>
      </div>
      <h5 class="counter-status">{{ evenOrOdd }}</h5>
    </section>

    <section class="title-edit">
      <label for="">Edit counter title</label>
      <input type="text" v-model="dataCount.title" />
    </section>
  </div>
</template>

<script setup>
import { computed, reactive, watch } from "vue";

const appTitle = "The Application Title";

const dataCount = reactive({
  count: 0,
  title: "My Counter Title",
});

watch(() => dataCount.count , (newCount, oldCount) => {

  if (newCount == 20) {
    alert('YOu are good to go, the current count is ' + newCount )
  }


});


const evenOrOdd = computed(() => {
  if (dataCount.count % 2 === 0) return 'Even' 
  return 'Odd'
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
  max-width: 400px;
  margin: 40px auto;
  padding: 20px;
  background-color: #f7f7f7;
  border: 1px solid #ddd;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

header {
  background-color: #333;
  color: #fff;
  padding: 10px;
  text-align: center;
  border-bottom: 1px solid #333;
}

h1 {
  font-size: 24px;
  margin-bottom: 10px;
}

h2 {
  color: darkslategray;
}

.counter-section {
  margin-top: 20px;
}

.counter-controls {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 10px;
}

.btn {
  font-size: 24px;
  padding: 10px 20px;
  min-width: 60px;
  margin: 10px;
  border: none;
  border-radius: 10px;
  cursor: pointer;
}

.btn-minus {
  background-color: #ff69b4;
  color: #fff;
}

.btn-plus {
  background-color: #34c759;
  color: #fff;
}

.counter {
  font-size: 36px;
  font-weight: bold;
  margin: 0 20px;
  color: black;
}

.counter-status {
  font-size: 18px;
  text-align: center;
  color: #666;
  margin-top: 10px;
  color: darkslategray;
}

.title-edit {
  margin-top: 20px;
}

label {
  display: block;
  margin-bottom: 10px;
}

input[type="text"] {
  padding: 10px;
  width: 100%;
  border: 1px solid #ccc;
  border-radius: 10px;
}
</style>