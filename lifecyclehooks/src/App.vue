<template>
<div id="app">

   <div id="success" class="alert alert-success" v-if="isSuccess">Successful login</div>
  <lifecycle />
<form @submit.prevent="getData">
    <div>
      NAME : <input type="text" name="name" placeholder="Username" required v-model="name">
    </div><br>
    <div>
      EMAIL : <input type="email" name="email" placeholder="@gmail.com" required v-model="email">
    </div><br>

    PHONE : <select name="code" >
      <option selected hidden>254</option>
      <option>254</option>
      <option>255</option>
      <option>256</option>
      <option>257</option>
      <input type="number"  required width="10" >
    </select><br>
    <br>
    <div>
      LOCATION : <input type="text" name="place" placeholder="Nairobi" required v-model="location">
    </div>
    <br>
    <div>
      TIME : <input type="date" required v-model="time">
    </diV>
    <br>
  <div>Current order
    <button @click="decreaseOrder" class="btn">-</button>
    <span class="order">{{order}}</span>
    <button @click="increaseOrder" class="btn">+</button>
  </div><br>
    <div id="btn" :class="click">
      <button type="button" class="ord">CANCEL</button>
      <button type="submit" @click="getData" class="ord">SUBMIT</button>
  </div>
  </form>

</div>
</template>

<script>
import lifecycle from './components/lifecycle.vue'

export default {
  name: 'App',
  components: {
    lifecycle
  },
  data(){
    return{
      name:'',
      email:'',
      PHONE:'',
      location:'',
      time:'',
      order:0,
      click:{
        active:true
      },
      isSuccess:false
    }
  },
  methods:{
    decreaseOrder(){
      this.order--;
    },
    increaseOrder(){
      this.order++;
    },
    async getData(){
      await fetch('https://jsonplaceholder.typicode.com/posts/App.json',{
        method: 'GET',})
        .then((response)=>{
          this.isSuccess = true;
          setTimeout(()=>{this.isSuccess},50)
          console.log(response)
        })
            .then(data=>console.log(data))

    }
  },
  watch:{
    order(newOrder){
      if(newOrder===10){
        alert('The Order has reaches maximum')
        }

      }
    }
}
</script>

<style>
*{
  text-align: center;
  background-color: rosybrown;
}
#app {

}
#success{
  color: red;
  font-size: 30px;
  font-weight: bold;
}
.btn, .order{
  font-size: 20px;
  margin: 7px;
}
.ord {
  font-size: 16px;
  font-weight: bold;
  color: blueviolet;
}
.ord:hover{
  color: red;
  cursor: pointer;
}
</style>
