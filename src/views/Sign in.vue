<template>
  <div class="signin">
    <div class="form-wrapper">
  <h1>Sign In</h1>
  <form @submit.prevent="handleSubmit">
    <div class="form-item">
      <label for="firstName"></label>
      <input v-model="form.firstName" type="text" name="firstName" required="required" placeholder="First Name" />
    </div>
    <div class="form-item">
      <label for="lastName"></label>
      <input v-model="form.lastName" type="text" name="lastName" required="required" placeholder="Last Name" />
    </div>
    <div class="form-item">
      <label for="email"></label>
      <input v-model="form.email" type="email" name="email" required="required" placeholder="Email Address" />
    </div>
    <div class="form-item">
      <label for="phone"></label>
      <input v-model="form.phone" type="text" name="phone" required="required" placeholder="Phone number" />
    </div>
    <div class="form-item">
      <label for="password"></label>
      <input v-model="form.password" type="password" name="password" required="required" placeholder="Password" />
    </div>
    <div class="form-item">
      <label for="address"></label>
      <input v-model="form.address" type="text" name="address" required="required" placeholder="address" />
    </div>
    <div class="form-item">
      <label for="building"></label>
      <input v-model="form.building" type="text" name="building" required="required" placeholder="building" />
    </div>
    <div class="form-item">
      <label for="postalCode"></label>
      <input v-model="form.postalCode" type="text" name="postalCode" required="postalCode" placeholder="postalCode" />
    </div>
    <div>
      <input type="radio" id="one" value="Private" v-model="form.type">
      <label for="one">Private</label>
      <input type="radio" id="two" value="Company" v-model="form.type">
      <label for="two">Company</label>
      <br>
      <br>
    </div>
    <div id='rolesSignIn'>
      <input type="checkbox" id="buyer" value="Buyer" v-model="form.roles">
      <label for="buyer">Buyer</label>
      <input type="checkbox" id="seller" value="Seller" v-model="form.roles">
      <label for="seller">Seller</label>
      <br>
    </div>
    <div class="button-panel">
      <input type="submit" class="button" title="Sign In" value="Sign In" />
    </div>
  </form>
  <div class="form-footer">
    <div class="button-panel" @click="goToLogIn">
    <button class="button">Go to Login</button></div>
  </div>
    <h2> {{ status }} </h2>
  </div>
</div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'signin',
  data () {
    return {
      form: {
        firstName: '',
        lastName: '',
        email: '',
        phone: '',
        address: '',
        building: '',
        postalCode: '',
        type: '',
        password: '',
        roles: []

      },
      responseData: {
        userId: '',
        firstName: '',
        lastName: '',
        email: '',
        phone: '',
        address: '',
        building: '',
        postalCode: '',
        type: ''
      },
      status: '',
      picked: ''
    }
  },
  methods: {
    goToLogIn () {
      this.$router.push({ name: 'login' })
    },
    handleSubmit: function () {
      this.status = 'Loading...'

      var vm = this

      let axiosConfig = {
        headers: {
          'Content-Type': 'application/json',
          'Accept': 'application/json'
        }
      }

      axios.post('https://itec2019rockthecode.herokuapp.com/users', this.form, axiosConfig)
        .then(function (response) {
          vm.responseData = response.data
          vm.status = 'Welcome ' + vm.responseData.firstName + ' ' + vm.responseData.lastName + '!'
        })
        .catch(function (error) {
          vm.status = error
          console.log(error.message)
        })
    }
  }
}
</script>

<style>
/* Fonts */
@import url(https://fonts.googleapis.com/css?family=Open+Sans:400);

/* fontawesome */
@import url(http://weloveiconfonts.com/api/?family=fontawesome);
[class*="fontawesome-"]:before {
  font-family: 'FontAwesome', sans-serif;
}

/* Simple Reset */
* { margin: 0; padding: 0; box-sizing: border-box; }

/* body */
body {
  background: #e9e9e9;
  color: #5e5e5e;
  font: 400 87.5%/1.5em 'Open Sans', sans-serif;
}

/* Form Layout */
.form-wrapper {
  background: #fafafa;
  margin: 3em auto;
  padding: 0 1em;
  max-width: 370px;
}

h1 {
  text-align: center;
  padding: 1em 0;
}

form {
  padding: 0 1.5em;
}

.form-item {
  margin-bottom: 0.75em;
  width: 100%;
}

.form-item input {
  background: #fafafa;
  border: none;
  border-bottom: 2px solid #e9e9e9;
  color: #666;
  font-family: 'Open Sans', sans-serif;
  font-size: 1em;
  height: 50px;
  transition: border-color 0.3s;
  width: 100%;
}

.form-item input:focus {
  border-bottom: 2px solid #c0c0c0;
  outline: none;
}

.button-panel {
  margin: 2em 0 0;
  width: 100%;
}

.button-panel .button {
  background: #f16272;
  border: none;
  color: #fff;
  cursor: pointer;
  height: 50px;
  font-family: 'Open Sans', sans-serif;
  font-size: 1.2em;
  letter-spacing: 0.05em;
  text-align: center;
  text-transform: uppercase;
  transition: background 0.3s ease-in-out;
  width: 100%;
}

.button:hover {
  background: #ee3e52;
}

.form-footer {
  font-size: 1em;
  padding: 2em 1.5em;
  text-align: center;
}

.form-footer a {
  color: #8c8c8c;
  text-decoration: none;
  transition: border-color 0.3s;
}

.form-footer a:hover {
  border-bottom: 1px dotted #8c8c8c;
}
</style>
