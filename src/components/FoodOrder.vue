<template>
  <div>
    <h1>Time To EAT</h1>
    <div class="wrapper-progress">
      <ul class="progress-bar">
        <li @click="index=0">Order</li>
        <li @click="index=1">Check</li>
        <li @click="index=2">Success</li>
      </ul>
    </div>
    <div class="content">
        <List v-if="index === 0" class="content-tab"></List>
        <Check v-else-if="index === 1" class="content-tab"></Check>
        <Success v-else-if ="index === 2" class="content-tab"></Success>
    </div>
    <div class="action">
      <Button @click="previosPage()" v-if="index>0">Back</Button>
      <button @click="nextPage()" v-if="index<2">Next</button>

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
  data(){
      return {
          foods:[
            {id: 1, name: 'Food A', price: 10},
            {id: 2, name: 'Food B', price: 11},
            {id: 3, name: 'Food C', price: 12},
            {id: 4, name: 'Food D', price: 13},
            {id: 5, name: 'Food E', price: 14}

          ],
          index: 0
      }
  },
  props: ["msg"],
  methods: {
    nextPage(){
      if(this.index < 2) this.index++;
    },
    previosPage(){
      if(this.index >= 0)this.index--;
    }
  },
  watch: {
    index: function(curr, prev){
      console.log(`Current: ${curr}, Previous: ${prev}`)
    }
  }
};
</script>

<style>
.wrapper-progress {
    width: 100%
    
}

.progress-bar{
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
    border: 1px solid #ddd;
    display: block;
    text-align: center;
    margin: 0 auto 10px;
    background-color: white
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
    color: dodgerblue;
}

.progress-bar li.active:before {
    border-color: dodgerblue;
    background-color: dodgerblue
}

.progress-bar li.active + li:after {
    background-color: dodgerblue;
}
</style>