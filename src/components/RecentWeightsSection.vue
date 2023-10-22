<template>
    <div>
        <div class="weight-history">
              <!-- <ul>
                <li v-for="weight in recentWeights" v-bind:key="date in recentWeights">
                  <span>{{ weight.weight }}kg</span>
                  <small>{{ new Date(weight.date).toLocaleDateString() }}</small>
                  </li>
        
                </ul> -->
              </div>
        <!-- <p>{{this.recentWeight}}</p> -->
    </div>
</template>

<script>
export default {
    name: 'Recent-Weight',
    props: {
    recentWeights: Array, 
   
  }, 
    mounted(){
// console.log(this.recentWeights, 'mounted')
    },
    updated(){
        // console.log(this.recentWeights, 'updated')
    }
  
}
</script>