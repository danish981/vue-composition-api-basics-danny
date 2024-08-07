## Danny | Udemy Course videos

### Current Chapter - 08 : VUE ROUTER

Video : 001

---

---

---

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

- custom direcities, we can create our own and use them in our code and use with life cycle hooks, for example this directive will highlight and focus the element where it is used and gain focus when the component is mounted

```js
<input type="text" v-autofocus />;

const vAutofocus = {
  mounted: (el) => {
    el.focus();
  },
};
```

- this is how we can create a custom js file and import it and use the funcitons inside of this, **MADE A GLOBAL CUSTOM DIRECTIVE**


```js

// the use in template
<input type="text" v-model="dataCount.title" v-autofocus />


// the import
import { vAutofocus } from "@/directives/vAutofocus";

// the code inside of a file
export const vAutofocus = {
  mounted: (el) => {
    el.focus()
  }
}


```


### Higher order function 

In JavaScript, `filter`, `map`, and `reduce` are higher-order functions that operate on arrays. They are part of the array prototype and are widely used for functional programming. Here's an overview of each:

### 1. **`filter` Method**
The `filter` method creates a new array with all elements that pass the test implemented by the provided function.

#### **Syntax:**
```javascript
const newArray = array.filter(callback(element[, index[, array]])[, thisArg]);
```

- **`callback`**: A function that is called for every element of the array. If it returns `true`, the element is kept; otherwise, it is removed.
- **`element`**: The current element being processed.
- **`index`**: (Optional) The index of the current element being processed.
- **`array`**: (Optional) The array `filter` was called upon.
- **`thisArg`**: (Optional) Value to use as `this` when executing `callback`.

#### **Example:**
```javascript
const numbers = [1, 2, 3, 4, 5, 6];
const evenNumbers = numbers.filter(number => number % 2 === 0);
console.log(evenNumbers); // Output: [2, 4, 6]
```

### 2. **`map` Method**
The `map` method creates a new array populated with the results of calling a provided function on every element in the calling array.

#### **Syntax:**
```javascript
const newArray = array.map(callback(element[, index[, array]])[, thisArg]);
```

- **`callback`**: A function that is called for every element of the array. It produces a new element for the new array.
- **`element`**: The current element being processed.
- **`index`**: (Optional) The index of the current element being processed.
- **`array`**: (Optional) The array `map` was called upon.
- **`thisArg`**: (Optional) Value to use as `this` when executing `callback`.

#### **Example:**
```javascript
const numbers = [1, 2, 3, 4, 5];
const squaredNumbers = numbers.map(number => number * number);
console.log(squaredNumbers); // Output: [1, 4, 9, 16, 25]
```

### 3. **`reduce` Method**
The `reduce` method executes a reducer function (that you provide) on each element of the array, resulting in a single output value.

#### **Syntax:**
```javascript
const result = array.reduce(callback(accumulator, currentValue[, index[, array]]), initialValue);
```

- **`callback`**: A function that is executed on each element of the array, taking four arguments:
  - **`accumulator`**: Accumulates the callback's return values. It is the accumulated value previously returned in the last invocation of the callback, or `initialValue`, if supplied.
  - **`currentValue`**: The current element being processed.
  - **`index`**: (Optional) The index of the current element being processed.
  - **`array`**: (Optional) The array `reduce` was called upon.
- **`initialValue`**: (Optional) A value to use as the first argument to the first call of the callback. If no initial value is supplied, the first element in the array will be used and skipped in the iteration.

#### **Example:**
```javascript
const numbers = [1, 2, 3, 4, 5];
const sum = numbers.reduce((accumulator, currentValue) => accumulator + currentValue, 0);
console.log(sum); // Output: 15
```

### **Summary:**
- **`filter`**: Use it to filter out elements that do not satisfy a condition.
- **`map`**: Use it to transform each element in the array.
- **`reduce`**: Use it to accumulate all elements of the array into a single result.

These methods can be chained together to perform complex transformations on arrays in a clean and readable way.



## Array destructuring 

Destructuring in JavaScript is a convenient way to extract values from arrays or properties from objects into distinct variables. It provides a concise syntax to unpack data from arrays or objects into individual variables.

### 1. **Array Destructuring**
Array destructuring allows you to unpack elements from an array into individual variables based on their position.

#### **Syntax:**
```javascript
const [variable1, variable2, ...rest] = array;
```

#### **Example:**
```javascript
const numbers = [1, 2, 3, 4, 5];

const [first, second] = numbers;
console.log(first);  // Output: 1
console.log(second); // Output: 2

const [one, , three] = numbers;
console.log(three);  // Output: 3

// Using rest parameter
const [firstNumber, ...restNumbers] = numbers;
console.log(restNumbers); // Output: [2, 3, 4, 5]
```

### 2. **Object Destructuring**
Object destructuring allows you to extract properties from an object into variables with matching names.

#### **Syntax:**
```javascript
const { key1, key2, ...rest } = object;
```

#### **Example:**
```javascript
const person = {
  name: 'John',
  age: 30,
  city: 'New York'
};

const { name, age } = person;
console.log(name); // Output: John
console.log(age);  // Output: 30

// Using rest parameter
const { name: personName, ...otherDetails } = person;
console.log(personName);  // Output: John
console.log(otherDetails); // Output: { age: 30, city: 'New York' }
```

### 3. **Default Values**
You can provide default values when destructuring. This is useful if the array or object doesn’t have the value you’re trying to destructure.

#### **Example:**
```javascript
const [a = 1, b = 2] = [10];
console.log(a); // Output: 10
console.log(b); // Output: 2

const { x = 5, y = 10 } = { x: 20 };
console.log(x); // Output: 20
console.log(y); // Output: 10
```

### 4. **Nested Destructuring**
You can destructure nested objects or arrays by following the structure of the data.

#### **Example:**
```javascript
const person = {
  name: 'John',
  address: {
    city: 'New York',
    zip: '10001'
  }
};

const { name, address: { city, zip } } = person;
console.log(city); // Output: New York
console.log(zip);  // Output: 10001
```

### 5. **Function Parameters Destructuring**
You can also use destructuring in function parameters to directly access properties or elements passed into the function.

#### **Example:**
```javascript
function printPerson({ name, age }) {
  console.log(`Name: ${name}, Age: ${age}`);
}

const person = { name: 'Alice', age: 25 };
printPerson(person); // Output: Name: Alice, Age: 25

function sum([a, b]) {
  return a + b;
}

console.log(sum([1, 2])); // Output: 3
```

### **Summary:**
Destructuring is a powerful feature that simplifies code by allowing you to unpack values from arrays or properties from objects into distinct variables. It is particularly useful when dealing with data structures where you need to extract specific values or properties.


