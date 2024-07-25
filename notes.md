- there are two ways we can make the properties reactive, by using _reactive_ and _ref_
- **reactive** can be used to make an object and its underlying things reactive
- **ref** can be used to make a single variable (property) reactive
- using this approach, the variable _counter_ is only available to template when return is added there in the setup function

```js
<script>
import { ref } from "vue";
export default {
  setup() {
    const counter = ref(0);

    return {
      counter
    }
  },
};
</script>

```

- we cannot use the ref object directly to modify its value, we have to write like this, the _value_ of the ref object and we dont need to use _this_ to refer the object

```js
const counter = ref(0);

function increaseCounter() {
  counter.value++;
}

return {
  counter,
  increaseCounter,
};
```

- we can write the function like

```js
function increaseCounter() {
  counter.value++;
}

return {
  counter,
  increaseCounter,
};
```

and

```js
const increaseCounter = () => {
  counter.value++;
};
return {
  counter,
  increaseCounter,
};
```

- the first way of writing the app in _Composition API_

```js
<template>
  <div class="home">
    <div>
      <button class="btn minus" @click="decreaseCounter">-</button>
      <span class="counter"> {{ counter }} </span>
      <button class="btn plus" @click="increaseCounter">+</button>
    </div>
  </div>
</template>

<script>
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
</script>



```

-
