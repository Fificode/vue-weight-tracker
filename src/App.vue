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
    <div class="chart-section">
      <canvas ref="weightChartEl"></canvas>
    </div>
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


import { ref, shallowRef, watch, nextTick } from 'vue'
import Chart from 'chart.js/auto'
export default {
  name: 'App',
  setup(){
        
        //Initialized an empty array so the inputed weights and date will be pushed into 
        const weights = shallowRef([])
        //Initialized the inputed weight to 0.0
        const weightInput = ref(0.0)
        //Initialized the input submitted to 0.0
        const submittedInput = ref(0.0)
        //Initialized the weight chart element to null
        const weightChartEl = shallowRef(null)

        const weightChart = shallowRef(null)
       
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

 watch (weights, newWeights  => {
  const ws = [newWeights, ...newWeights]
console.log(weights, 'weights');
// console.log(ws);
if(weightChart.value){
    weightChart.value.data.labels = ws
        .sort((a,b) => a.date - b.date)
        .map(w  => new Date(w.date).toLocaleDateString())
        .slice(-7)

    weightChart.value.data.datasets[0].data = ws
        .sort((a,b) => a.date - b.date)
        .map(w  => w.weight) 
        .slice(-7)

        weightChart.value.update()
        // console.log(ws, 'ws') 

        return
        
  }
  nextTick(() => {
    console.log(weightChartEl, 'Weight chart Element');
    console.log(weightChartEl.value, 'Weight chart Element Value');
    weightChart.value = new Chart(weightChartEl.value.getContext('2d'),
    {
      type: 'line',
      data: {
        labels: ws
        .sort((a,b) => a.date - b.date)
        .map(w  => new Date(w.date).toLocaleDateString()),
        datasets: [
          {
            label: 'Weight',
            data: ws
            .sort((a,b)=> a.date - b.date)
            .map(w => w.weight),
            backgroundColor: 'rgba(255, 105, 180, 0.2)',
            borderColor: 'rgb(255, 105, 180)',
            borderWidth: 1,
            fill: true
          }
        ]
      },
      options: {
        responsive: true,
        maintainAspectRatio: false
      }
    })
  })
  
 }
 , {immediate: true})
//  console.log(weightChart, 'weight chart')


return {
            weights,
            weightInput,
            submittedInput,
            addWeight,
            weightChart,
            weightChartEl
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
  color: #888;
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
    border: none;
    appearance: none;
    font-size: 17px;
}
.input-submit{
  border: none;
    border-radius: 3px;
    height: 35px;
    margin-top: 10px;
    width: 50%;
    cursor: pointer;
    background-color: blueviolet;
    outline-color:#fff ;
    color: #fff;

}
.input-submit:hover{
border-color: purple;
border-width: 2px;
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
.chart-section{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100%;
  /* background-color: #fff; */
  padding: 20px;
  border-radius: 2px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  margin-bottom: 10px;
  margin-top: 10px;
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
