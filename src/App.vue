<template>
  <div id="app">
    <h1>Our Team</h1>
  <EmployeeList />


  </div>

</template>

<script>
import EmployeeList from './components/EmployeeList.vue';


export default {
  name: 'App',

  components: {
    EmployeeList,

  }
}
</script>

<style>
 @import './assets/style.css';
</style>