<template>
  <div class="home">
    <div>
      <button class="btn minus" @click="decreaseCounter">-</button>
      <span class="counter"> {{ counter }} </span>
      <button class="btn plus" @click="increaseCounter">+</button>
    </div>
  </div>
</template>



<!-- there are two patterns to write the code in composition API -->
<script>
export default {
  setup() {

  }
}
</script>




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