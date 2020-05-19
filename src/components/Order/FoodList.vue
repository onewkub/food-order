<template>
  <div>
    <h1>Order</h1>
    <div class="foodList">
      <ul>
        <li v-for="food in foodList" :key="food.id">
          <div
            class="food-selector"
            :class="{selected: food.marked,unSelected: !food.marked}"
            @click="toggleFood(food)"
          >
            <div class="name">{{food.name}}</div>
            <div class="price">Price: {{food.price}}$</div>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "List",
  props: ["foodList"],
  data() {
    return {};
  },
  methods: {
    toggleFood(food) {
      this.$emit("markFood", food);
    }
  }
};
</script>

<style>
ul {
  width: 100%;
  padding: 0;
}
li {
  color: white;
  list-style-type: none;
}
.food-selector {
  width: 40%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 1.2rem;
  height: 3.6rem;
  margin: 0.2rem auto;
  cursor: pointer;
  border: rgba(252, 239, 67, 0.5) solid 0.05rem;
}

.unSelected {
  background-color: #353333e3;
}
.unSelected:hover {
  background-color: #444343;
}

.unSelected:active {
  background-color: #292929e0;
}

.selected {
  background-color: #dbbd35;
}
.selected:hover {
  background-color: #f0d24bef;
}
.selected:active{
  background-color: #9b8629;

}
</style>