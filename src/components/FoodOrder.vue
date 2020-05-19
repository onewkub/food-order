<template>
  <div>
    <h1>Time To EAT</h1>
    <div class="wrapper-progress">
      <ul class="progress-bar">
        <li :class="{active: index>=0}" @click="index=0">Order</li>
        <li :class="{active: index>=1}" @click="index=1">Check</li>
        <li :class="{active: index>=2}" @click="index=2">Success</li>
      </ul>
    </div>
    <div class="content">
        <List v-if="index === 0" class="content-tab" :foodList="markedFood" @markFood="markToggle"></List>
        <Check v-else-if="index === 1" class="content-tab" :selectedList="selectedFood" @addFood="addFood" @removeFood="removeFood"></Check>
        <Success v-else-if="index === 2" class="content-tab"></Success>
    </div>
    <div class="action">
      <Button @click="previosPage()" v-if="index>0 && index !== 2">Back</Button>
      <button @click="nextPage()" v-if="index<2">Next</button>
      <button @click="index = 0" v-if="index===2">Back to Order</button>
    </div>
  </div>
</template>

<script>
import List from "./Order/FoodList";
import Check from "./Order/FoodCheck";
import Success from "./Order/FoodSuccess";
export default {
  name: "FoodOrder",
  components: {
    List,
    Check,
    Success
  },
  data() {
    return {
      foods: [
        { id: 1, name: "Food A", price: 10 },
        { id: 2, name: "Food B", price: 11 },
        { id: 3, name: "Food C", price: 12 },
        { id: 4, name: "Food D", price: 13 },
        { id: 5, name: "Food E", price: 14 }
      ],
      index: 0,
      selectedFood: [],
      markedFood:[],
      total: 0
    };
  },
  props: [],
  methods: {
    nextPage() {
      if (this.index < 2) this.index++;
      if(this.index === 1) this.initSelectedFood();
    },
    previosPage() {
      if (this.index >= 0) this.index--;
    },
    addFood(food){
      food.ea++;
      this.calTotal()
    },
    removeFood(food){
      if(food.ea> 0){
        food.ea--;
        this.calTotal();
      }
    },
    initMarkedFood(){
      this.markedFood = this.foods.map(food => {return {...food, marked: false}})
    },
    initSelectedFood(){
      this.selectedFood = this.markedFood.filter(food => food.marked).map(food=> {{return {...food, ea: 1}}});
    },
    markToggle(food){
      food.marked = !food.marked;
      // console.log(`${food.name}: ${food.marked}`);
    },
    calTotal(){
      this.total = this.selectedFood.reduce(food=>food.price*food.ea, 0);
      console.log(this.total);
    }
  },
  created(){
    this.initMarkedFood();
  },
  updated(){
    this.calTotal();
  },
  watch: {
    // index: function(curr, prev) {
    //   console.log(`Current: ${curr}, Previous: ${prev}`);
    // },
    // selectedFood: function(curr, prev){
    //   console.log(curr);
    //   console.log(prev)
    // },
    // markedFood: function(curr){
    //   console.log(curr);
    // },
    // total: function(curr, prev){
    //   console.log(`current: ${curr}, previous: ${prev} `);
    // }
  }
};
</script>

<style>
.content{
  min-height: 20vh;
}
.wrapper-progress {
  width: 100%;
}

.action button{
  color: white;
  border: none;
  padding: 1rem 0;
  margin: 0 0.25rem;
  width: 7.2rem;
  background-color:#dbbd35;;
}

.action button:hover{
  background-color: #f0d24bef;
}

.action button:active{
  background-color: #9b8629;
}
.progress-bar {
  display: flex;
  justify-content: space-between;
  padding: 0;
}
.progress-bar li {
  width: 100%;
  list-style-type: none;
  position: relative;
  text-align: center;
  cursor: pointer;
}

.progress-bar li:before {
  content: " ";
  line-height: 30px;
  border-radius: 50%;
  width: 30px;
  height: 30px;
  border: 1px solid rgba(221, 221, 221, 0.85);
  display: block;
  text-align: center;
  margin: 0 auto 10px;
  background-color: rgba(255, 255, 255, 1);
}

.progress-bar li:after {
  content: "";
  position: absolute;
  width: 100%;
  height: 2px;
  background-color: #ddd;
  top: 15px;
  left: -50%;
  z-index: -1;
}

.progress-bar li:first-child:after {
  content: none;
}

.progress-bar li.active {
  color: rgba(255, 255, 255, 0.85);
}

.progress-bar li.active:before {
  border-color: rgba(252, 239, 67, 0.85);
  background-color: rgba(252, 239, 67, 1);
}

.progress-bar li.active + li:after {
  background-color: rgba(252, 239, 67, 1);
}
</style>