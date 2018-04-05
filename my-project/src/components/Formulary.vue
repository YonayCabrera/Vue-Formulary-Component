<template>
  <div>
      <h1>Heii</h1>
      <form action=""> 
          <input v-model="objeto.name" v-if="email" type="text" placeholder="name">
          <input v-model="objeto.email" v-if="username" type="email" placeholder="email">
          <input v-model="objeto.phone" v-if="tel" type="text" placeholder="phone">
          <input v-model="objeto.password" v-if="pass" type="password" placeholder="password">
          <input v-model="objeto.verify" v-if="verifyPass" type="password" placeholder="verifyPass">
          <button @click="$emit('completed', objeto)" type="button">accept</button>
      </form>
  </div>
  
</template>
<script>
export default {
  data() {
    return {
    };
  },
  props: ['email','username','tel', 'pass', 'verifyPass', 'objeto'],
  watch: {
    'objeto.name': function () {
      console.log(this.objeto.name)
    }
  }
};
</script>
<style scoped>
input {
    display: block;
}

</style>


