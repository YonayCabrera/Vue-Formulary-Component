<template>
  <div id="app">
    <Formulary 
      :objeto="user" 
      @completed="signUp"
      :email="true"
      :username="true"
      :tel="true"
      :pass="true"
      :verifyPass="true"
      :materialize="true"
      :bootstrap="false"
    />
  </div>
</template>

<script>
import Formulary from './components/Formulary';

export default {
  name: 'App',
  data() {
    return {
      user:{}
    }
  },
  components: {
    Formulary,
  },
  methods: {
    signUp(user){
      console.log(JSON.stringify(user))
    }
  }
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
