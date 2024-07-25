<template>
  <div class="home">
    <div>
      <button class="btn minus" @click="decreaseCounter">-</button>
      <span class="counter"> {{ counter }} </span>
      <button class="btn plus" @click="increaseCounter">+</button>
    </div>
  </div>
</template>




<script setup>
import { ref } from "vue";
const counter = ref(0);
</script>






<!-- USING THE CLASSIC COMPOSITION API PATTERN  -->
<!-- <script>
import { ref } from "vue";
export default {
  setup() {
    const counter = ref(90);

    const increaseCounter = () => {
      counter.value++;
    };

    const decreaseCounter = () => {
      if (counter.value > 0) counter.value--;
    };

    return {
      counter,
      increaseCounter,
      decreaseCounter,
    };
  },
};
</script> -->





<!-- USING THE OPTIONS API -->
<!-- <script>
export default {
  data() {
    return {
      counter: 0,
    };
  },
  methods: {
    increaseCounter() {
      this.counter++;
    },
    decreaseCounter() {
      if (this.counter > 0) this.counter--;
    },
  },
};
</script> -->



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