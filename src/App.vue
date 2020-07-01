<template>
<form id="app" @submit="checkForm" action="/something" method="post" novalidate="true">
  
  <p v-if="errors.length">
    <b>Please correct the following error(s):</b>
    <ul>
      <li v-bind:key="error" v-for="error in errors">{{ error }}</li>
    </ul>
  </p>
  
  <p>
  <label for="name">First Name</label>
  <input type="text" name="name" id="name" v-model="name">
  </p>

  <p>
  <label for="age">Age</label>
  <input type="number" name="age" id="age" v-model="age">
  </p>

  <p>
  <label for="email">Email</label>
  <input type="email" name="email" id="email" v-model="email">
  </p>

  <p>
  <label for="movie">Favorite Website</label>
  <select name="website" id="website" v-model="website">
    <option>Google</option>
    <option>W3 Schools</option>
    <option>Code Academy</option>
    <option>Meet Up</option>
  </select>
  </p>

  <p>
  <input type="submit" value="Submit">  
  </p>

</form>
</template>

<script>
export default {
  name: 'App',

  el:'app',
  data: function() {
    return {
    errors:[],
    name:null,
    age:null,
    email:null,
    website:null
    }
  },
  methods:{
    checkForm:function(e) {
      this.errors = [];
      if(!this.name) this.errors.push("Name is required");
      if(!this.email) {
        this.errors.push("Email is required");
      } else if (!this.validEmail(this.email)) {
        this.errors.push("This is not a valid email address");
      }
      if(!this.age) this.errors.push("Age is required");
      if(Number(this.age) < 18) this.errors.push("Need to be over 18");
      if(!this.errors.length) return true;
      e.preventDefault();
      },
      validEmail: function(email) {
        var regexEmail = /^\w+([-+.']\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*$/;
        return regexEmail.test(email);
      }
  }
}
</script>

<style>
#app {
  font-family: Verdana, Helvetica, Arial, sans-serif;
  color: #0000ff;
  margin-top: 40px;
  background-color: lightblue;
}
</style>
