<template>
  <div>
    <header class='header'>
      <h1>Weight Tracker App</h1>
    </header>
    <main>
      <div>
    <div class="current">
      <h3>{{ submittedInput }}</h3>
      <h4>Current weight (kg)</h4>
      </div>
    <form @submit.prevent="addWeight" class="form">
        <input type="number" step="0.1" v-model="weightInput" class="input-number"/><br/>
        <input type="submit" value="Add weight" class="input-submit"/>
        </form>
</div>
    </main>
    
    <h2>Last 7 days</h2>
    <ChartSection/>
    <h2>Weight History</h2>
    <RecentWeightsSection :recentWeights="weights.value"/> 
  </div>
</template>

<script>

import RecentWeightsSection from './components/RecentWeightsSection.vue';
import ChartSection from './components/ChartSection.vue';


import { ref, shallowRef } from 'vue'
export default {
  name: 'App',
  components: {
    
    RecentWeightsSection,
    ChartSection
   
  },
  setup(){
        
        //Initialized an empty array so the inputed weights and date will be pushed into 
        const weights = shallowRef([])
        //Initialized the inputed weight to 0.0
        const weightInput = ref(0.0)
        const submittedInput = ref(0.0)
        let weightsValue = shallowRef([])

const addWeight = () => {
    //Show weight on screen
submittedInput.value = weightInput.value;
//  weightsValue = weights.value
//Add weight and date to an array
 weights.value.push({
    weight: submittedInput.value, 
    date: new Date().getTime()
   })
  //  console.log(weights.value)
  //  if(weights.value.length > 0 ){
  //  weights.value.sort((a,b) => b.date - a.date)
  // }
        }

return {
            weights,
            weightInput,
            weightsValue,
            submittedInput,
            addWeight,
           
         
            
        }
    },
  
 
}
</script>

<style >
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
}
h2{
 text-align: center;
  padding-top: 50px;
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
    height: 30px;
    padding: 5px;
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
.current{
    margin-top: 60px;
    margin-bottom: 30px;
}
</style>
