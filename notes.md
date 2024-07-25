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

- refs returned from setup are automatically shallow unwrapped when accessed in the template so you do not need to use ._value_ when accessing them

- Think of MyComponent as being referenced as a variable. If you have used JSX, the mental model is similar here. The kebab-case equivalent `<my-component>` also works in the template - however PascalCase component tags are strongly recommended for consistency. It also helps differentiating from native custom elements.

- If you have a named import that conflicts with the component's inferred name, you can alias the import:

```js
import { FooBar as FooBarChild } from "./components";
```

- **Namespaced Components** : You can use component tags with dots like `<Foo.Bar>` to refer to components nested under object properties. This is useful when you import multiple components from a single file:

```js
<script setup>
import * as Form from './form-components'
</script>

<template>
  <Form.Input>
    <Form.Label>label</Form.Label>
  </Form.Input>
</template>
```

-
