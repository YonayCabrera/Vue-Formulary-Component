<template>
  <div>
      <h1>Heii</h1>
      <form action=""> 
          <input v-model="objeto.name" v-if="username" type="text" placeholder="name">
          <input v-model="objeto.email" v-if="email" type="email" placeholder="email">
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
      regexName: /\b[a-zA-ZÁÉÍÓÚáéíóúÄËÏÖÜäëïöü\s]+\b/,
      regexEmail: /\w+@\w+/,
      regexPhone: /\(?([0-9]{3})\)?([ .-]?)([0-9]{3})\2([0-9]{4})/,
      regexPassword: /^(?=.*\d)(?=.*[a-z])(?=.*[A-Z])[0-9a-zA-Z]{8,}$/
    };
  },
  props: ["email", "username", "tel", "pass", "verifyPass", "objeto"],
  watch: {
    "objeto.name": function() {
      this.validaReg(this.objeto.name, this.regexName);
    },
    "objeto.email": function() {
      this.validaReg(this.objeto.email, this.regexEmail);
    },
    "objeto.phone": function() {
      this.validaReg(this.objeto.phone, this.regexPhone);
    },
    "objeto.password": function() {
      this.validaReg(this.objeto.password, this.regexPassword);
    },
    "objeto.verify": function() {
      this.verifyPassWord(
        this.objeto.verify,
        this.objeto.password,
        this.regexPassword
      );
    }
  },
  methods: {
    validaReg(user, exprex) {
      if (!user.match(exprex)) {
        console.log("NoesValido");
      } else {
        console.log("esValido");
      }
    },
    verifyPassWord(passwordToVerify, password, exprex) {
      if (passwordToVerify.match(exprex) && passwordToVerify == password) {
        console.log("esValido");
      } else {
        console.log("NoesValido");
      }
    }
  }
};
</script>
<style scoped>
input {
  display: block;
}
</style>


