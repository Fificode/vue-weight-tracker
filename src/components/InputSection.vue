<template>
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
</template>

<script>
import { ref, shallowRef } from 'vue'

export default{
    name: 'Input-Section',
    setup(){
        
        //Initialized an empty array so the inputed weights and date will be pushed into 
        const weights = shallowRef([])
        //Initialized the inputed weight to 0.0
        const weightInput = ref(0.0)
        const submittedInput = ref(0.0)

        
        const addWeight = () => {
    //Show weight on screen
submittedInput.value = weightInput.value;
//Add weight and date to an array
weights.value.push({
    weight: submittedInput.value, 
    date: new Date().getTime()
   }) 
console.log(weights.value)
        }

    
function currentWeight(){
   
    weights.value.sort((a,b) => b.date - a.date) || {weight: 0}
        }

   
        return {
            weights,
            weightInput,
            submittedInput,
            addWeight,
            currentWeight,
         
            
        }
    },
   
          }
</script>

<style scoped>
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
    color: #fff;

}
.current{
    margin-top: 60px;
    margin-bottom: 30px;
}
</style>