<template>
<div>
    <input type="text" placeholder="fruit" v-model="fruit.name">
  <input type="text" placeholder="price" v-model.number="fruit.price">
  <input type="text" placeholder="how many" v-model.number="fruit.count">
  <button :disabled="!fruitIsValid" @click="addFruit">addFruit</button>
  <div v-for="fruit in fruits">
      <div>
        <span>{{fruit.name}}</span>
        <span>{{fruit.price}}</span>
        <span>{{fruit.count}}</span>
        <button @click="removeFruit(fruit.name)">removeFruit</button>
      </div>
  </div>
  <div>
    <span>Precio Total: {{TotalPrice}}</span>
    <button @click="cancel">Cancel</button>
  </div>
</div>
</template>

<script>
export default {
  data() {
    return {
      fruit: {
        name: "",
        price: "",
        count: ""
      },
      fruits: []
    };
  },
  methods: {
    addFruit() {
      this.fruits.push(this.fruit);
      this.fruit = { name: "", price: "", count: "" };
    },
    removeFruit(name) {
      this.fruits = this.fruits.filter(fruit => fruit.name != name);
    },
    cancel() {
      this.fruits = [];
    }
  },
  computed: {
    fruitIsValid: function() {
      if (this.fruit.name.length > 3) {
        return true;
      }
      return false;
    },
    TotalPrice() {
      var total = 0;
      this.fruits.forEach(fruit => (total += fruit.price * fruit.count));
      return total;
    }
  }
};
</script>

<style>

</style>
