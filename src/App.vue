<template>
  <div>
    <header class='header'>
      <h1>Weight Tracker App</h1>
    </header>
    <InputSection />
    <ChartSection />
  </div>
</template>

<script>
import InputSection from './components/InputSection.vue';
import ChartSection from './components/ChartSection.vue';

export default {
  name: 'App',
  components: {
    InputSection,
    ChartSection,
  }
}
</script>

<style>
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
</style>
