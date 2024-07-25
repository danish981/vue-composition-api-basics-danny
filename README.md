## Danny | Udemy Course videos

### Current Chapter - 07 : Directives

Video : 001

---------------------------------------------------------------------
---------------------------------------------------------------------
---------------------------------------------------------------------

### NOTES 

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

- The two ways of writing composition API code vuejs APP

```js

// we can write the composition API code like this
<script>
export default {
  setup() {

  }
}
</script>


// but the actual and nicer and superior way is
<script setup>

</script>
```

- While using _reactive_ , we dont need to write the value, we say

```js
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


```

- we can also write the same method like

```js
const increaseCounter = (amount) => {
  dataCount.count += amount;
};

const increaseCounter = (amount) => {
  dataCount.count += amount;
};
```

- In JavaScript, destructuring is a syntax feature that allows you to extract values from arrays or objects and assign them to separate variables. It's a concise way to unpack values from a data structure and use them individually.

**Array Destructuring**

Let's start with an example of array destructuring:

```js
const colors = ["red", "green", "blue"];

const [firstColor, secondColor, thirdColor] = colors;

console.log(firstColor); // "red"
console.log(secondColor); // "green"
console.log(thirdColor); // "blue"
```

In this example, we have an array colors with three elements. We use the destructuring syntax [firstColor, secondColor, thirdColor] to extract the values from the array and assign them to separate variables. The variables are assigned in the order they appear in the array.

Object Destructuring

Now, let's look at an example of object destructuring:

```js
const person = { name: "John", age: 30, occupation: "Developer" };

const { name, age } = person;

console.log(name); // "John"
console.log(age); // 30
```

In this example, we have an object person with three properties. We use the destructuring syntax { name, age } to extract the values of the name and age properties and assign them to separate variables.

Nested Destructuring

You can also use destructuring with nested data structures:

```js
const address = {
  street: "123 Main St",
  city: "Anytown",
  state: "CA",
  zip: "12345",
  coordinates: {
    lat: 37.7749,
    lng: -122.4194,
  },
};

const {
  street,
  coordinates: { lat, lng },
} = address;

console.log(street); // "123 Main St"
console.log(lat); // 37.7749
console.log(lng); // -122.4194
```

In this example, we have an object address with a nested coordinates object. We use destructuring to extract the street property and the lat and lng properties from the coordinates object.

Default Values

You can also specify default values in case the property doesn't exist in the data structure:

```js
const person = { name: "John" };

const { name, age = 25 } = person;

console.log(name); // "John"
console.log(age); // 25
```

In this example, we specify a default value of 25 for the age property. Since the age property doesn't exist in the person object, the default value is used.

Destructuring is a powerful feature in JavaScript that can simplify your code and make it more expressive. It's widely used in modern JavaScript development.

- computer property use a reactive value, it cached, and updates when dependency is changed, it works only with the reactive data, it takes get and set if it needs to use something to get and set , but set is used rarely, see the docs https://vuejs.org/guide/essentials/computed.html#computed-properties

- with the _watch_, we cannot use the reactive property defined with _reactive_ directly, but we do with a getter , this is how we can watch for a value in the reactive value, so because it is _reactive()_ property we are doing the getter typed syntax, otherwise we can directly use the state defined with _ref_

```js
const dataCount = reactive({
  count: 0,
  title: "My Counter Title",
});

watch(
  () => dataCount.count,
  (newCount, oldCount) => {
    console.log(newCount, oldCount);
  }
);
```

and

```js
// like here, oldCount is not used, so we can remove it
// these both params hold the new and old value
watch(
  () => dataCount.count,
  (newCount, oldCount) => {
    if (newCount == 20) {
      alert("YOu are good to go, the current count is " + newCount);
    }
  }
);
```

- Lifecycle hooks like `mounted()` and `unmounted()` are the event names when triggered and we perform some action, see docs https://vuejs.org/api/composition-api-lifecycle.html#onmounted

- activated and deactivated hooks - keep alive caches the components

  https://vuejs.org/api/composition-api-lifecycle.html#onactivated
  https://vuejs.org/api/built-in-components.html#keepalive

- hooks fired just and after the data is updated on the component

```js
onBeforeUpdate(() => {
  console.log("onbeforeupdate");
});

onUpdated(() => {
  console.log("onupdated");
});
```

- we can use hooks on specific property , variable like what happen to the particular value if the component is mounted etc , read docs

- 


