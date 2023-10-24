<template>
  <div>
    <header class='header'>
      <h1>Weight Tracker App</h1>
    </header>
    <main class="main">
      <div class="current-container">
    <div class="current">
      <h3>{{ submittedInput }}</h3>
      <h4>Current weight (kg)</h4>
      </div>
    </div>
    <form @submit.prevent="addWeight" class="form">
        <input type="number" step="0.1" v-model="weightInput" class="input-number"/><br/>
        <input type="submit" value="Add weight" class="input-submit"/>
        </form>

<div v-if="weights && weights.length > 0">
           <h2>Recent Weights</h2>
    <ChartSection/>
    <h2>Weight History</h2>
    <ul>
                <li v-for="weight in weights" v-bind:key="weight.date" class="weight-list">
                  <span>{{ weight.weight }}kg</span>
                  <small>{{ new Date(weight.date).toLocaleDateString() }}</small>
                  </li>
                </ul>
    
   </div>
    </main>
    
  </div> 
</template>

<script>


import ChartSection from './components/ChartSection.vue';


import { ref, shallowRef } from 'vue'
export default {
  name: 'App',
  setup(){
        
        //Initialized an empty array so the inputed weights and date will be pushed into 
        const weights = shallowRef([])
        //Initialized the inputed weight to 0.0
        const weightInput = ref(0.0)
        //Initialized the input submitted to 0.0
        const submittedInput = ref(0.0)
       
 //Show weight on screen
const addWeight = () => {
  //updated the submitted input to the weight input 
submittedInput.value = weightInput.value;

//Add weight and date to an empty array
  weights.value.push({
    weight: submittedInput.value, 
    date: new Date().getTime()
   })
  //Sorted the date so the most recent date is on top
   weights.value.sort((a,b) => b.date - a.date)
 }

return {
            weights,
            weightInput,
            submittedInput,
            addWeight,
           }
    },
  }
  
</script>

<style >
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  margin: 0;
  background: #fff;
  background: radial-gradient(879px at 10.4% 22.3%, rgb(255, 235, 238) 0%, rgb(186, 190, 245) 93.6%);
  background-attachment: fixed;
  min-height: 100vh;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
 h1{
  text-align: center;
  font-size: 30px;
}
h2{
 text-align: center;
  padding-top: 50px;
  font-size: 20px;
}
h3{
  font-size: 25px;
  padding: 5px 0;
}
.form{
   display: flex;
   flex-direction: column;
   justify-content: center; 
   align-items: center;
}
input{
    border: 1px solid #ddd;
    }
.input-number{
    border-radius: 2px;
    width: 70%;
    height: 40px;
    padding: 10px 5px;
    outline-color:blueviolet ;
}
.input-submit{
    border-radius: 3px;
    height: 35px;
    margin-top: 10px;
    width: 50%;
    cursor: pointer;
    background-color: blueviolet;
    outline-color:#fff ;
    color: #fff;

}
.current-container{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.current{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
background-color: #fff;
margin: 30px 0;
    border-radius: 50%;
    width: 180px;
    height: 180px;
    border: 5px solid blueviolet;
}
.main{
  margin: 0;
  padding: 20px;
}
.main ul{
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.weight-list{
  border: 1px solid purple;
  border-radius: 5px;
  background-color: #fff;
  list-style: none;
  text-align: center;
  padding: 10px;
  width: 60%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 10px 0;
}
.weight-list span{
  font-size: 18px;
  font-weight: 700;
}
.weight-list small{
  font-size: 15px;
  font-weight: 600;
}
</style>
