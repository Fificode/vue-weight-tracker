<template>
<div>
    <div class="current">
      <h3>{{ currentWeight.weight }}</h3>
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
        // const weights = ref([])
        const weights = shallowRef([])
        const weightInput = ref(0.0)
        
    function addWeight(){ 
        
    weights.value.push({
    weight: weightInput.value, 
    date: new Date().getTime()
   
}) 
console.log(weights.value[0])
} 

function currentWeight(){
   
    weights.value.sort((a,b) => b.date - a.date)[0] || {weight: 0}
        }

   
        return {
            weights,
            weightInput,
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