<template>
<div >
  <div class="withOutStyle" v-if="false">
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
  <div class="row grid-wrapper" v-if="materialize">
        <form class="col s12">
            <div class="row">
                <div class="input-field col s6">
                    <i class="material-icons prefix">account_circle</i>
                    <input v-model="objeto.name" v-if="username" id="username" type="text" class="validate">
                    <label for="username">username</label>
                </div>
                <div class="input-field col s6">
                    <i class="material-icons prefix">phone</i>
                    <input v-model="objeto.phone" v-if="tel" id="icon_telephone" type="tel" class="validate">
                    <label for="icon_telephone">Telephone</label>
                </div>
            </div>
            <div class="row">
                <div class="input-field col s12">
                    <input v-model="objeto.email" v-if="email" id="email" type="email" class="validate">
                    <label for="email">Email</label>
                </div>
            </div>
            <div class="row">
                <div class="input-field col s6">
                    <input v-model="objeto.password" v-if="pass" id="password" type="password" class="validate">
                    <label for="password">Password</label>
                </div>
                <div class="input-field col s6">
                    <input v-model="objeto.verify" v-if="verifyPass" id="Verify" type="password" class="validate">
                    <label for="Verify">Verify Password</label>
                </div>
            </div>
            <div class="row">
                <button @click="$emit('completed', objeto)" class="btn waves-effect waves-light" type="submit" name="action">Submit
                    <i class="material-icons right">send</i>
                </button>

            </div>
    </form>
    </div>
    <div v-if="bootstrap">
     <h1>Formularios</h1>
     <form action="">
           <div class="form-row">
           <div class="form-group col-md-6 offset-md-3">
           <label for="inputname4">Nombre</label>
           <input v-model="objeto.name" v-if="username" type="email" class="form-control" placeholder="Nombre">
           </div>
           <div class="form-group col-md-6 offset-md-3">
           <label for="inputEmail4">Email</label>
           <input v-model="objeto.email" v-if="email" type="email" class="form-control" placeholder="Email">
           </div>
           <div class=" form-group col-md-6 offset-md-3">
           <label for="inputPhone4">Telefono</label>
           <input v-model="objeto.phone" v-if="tel" type="email" class="form-control" placeholder="Telefono">
           </div>
       </div>
       <div class="form-row">
           <div class="form-group col-md-6 offset-md-3">
           <label for="inputPassword4">Password</label>
           <input v-model="objeto.password" v-if="pass" type="password" class="form-control" placeholder="Password">
           </div>
           <div class="form-group col-md-6 offset-md-3">
           <label for="inputVerifyPassword4">Verificar Password</label>
           <input v-model="objeto.verify" v-if="verifyPass" type="password" class="form-control" placeholder="Password">
           </div>
       </div>
       <button @click="$emit('completed', objeto)" type="button" class="btn btn-primary">Submit</button>
       </form>      
 </div>
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
  props: ["email", "username", "tel", "pass", "verifyPass", "objeto", "materialize", "bootstrap"],
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
.grid-wrapper {
  display: grid;
  grid-template-columns: minmax(1em, 1fr) minmax(0, 50em) minmax(1em, 1fr);
}
.grid-wrapper form {
  grid-column: 2;
}
.withOutStyle input {
  display: block;
}
</style>


