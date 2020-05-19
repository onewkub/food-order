<template>
  <div>
    <h1>Check</h1>
    <div class="foodList">
      <ul>
        <li v-for="food in selectedList" :key="food.id">
          <div class="food-selector">
            <div class="name">{{food.name}}</div>
            <div class="price">Price: {{food.price}}$</div>
            <div class="ea">
              <button class="remove" @click="removeFood(food)">-</button>
              <span>{{food.ea}}</span>
              <button class="add" @click="addFood(food)">+</button>
            </div>
          </div>
        </li>
      </ul>
    </div>
    <h2>Total: {{total}}</h2>
  </div>
</template>

<script>
export default {
  name: "Check",
  props: ["selectedList", "total"],
  data() {
    return {
    };
  },
  methods: {
    addFood(food) {
      console.log(food);
      this.$emit("addFood", food);
    },
    removeFood(food) {
      console.log(food);
      this.$emit("removeFood", food);
    }
  }
};
</script>

<style scoped>
ul{
  width: 100%;
  padding: 0;
}
li{
  color: white;
  list-style-type: none;
}
.food-selector{
  width: 40%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 1.2rem;
  height: 3.6rem;
  margin: 0.2rem auto;
  cursor: pointer;
  background-color: #353333e3;
  border: rgba(252, 239, 67, 0.5) solid 0.05rem;
}

.food-selector .ea{
  display: flex;
  align-items: center;
}

.food-selector .ea button{
  border: none;
  color: white;
  cursor: pointer;
  width: 2rem;
  height: 2rem;
}
.food-selector .ea .add{
  background-color: green;
}

.food-selector .ea .remove{
  background-color: red;
}


.food-selector .ea span{
  margin: 0 0.5rem;
}
</style>