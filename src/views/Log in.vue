<template>
  <div class="login">
    <div class="form-wrapper">
  <h1>Log In</h1>
  <form @submit.prevent="handleSubmit">
    <div class="form-item">
      <label for="email"></label>
      <input v-model="form.email" type="email" name="email" required="required" placeholder="Email Address" />
    </div>
    <div class="form-item">
      <label for="password"></label>
      <input v-model="form.password" type="password" name="password" required="required" placeholder="Password" />
    </div>
    <div class="button-panel">
      <input type="submit" class="button" title="Log In" value="Log In" />
    </div>
  </form>
  <div class="form-footer">
    <div class="button-panel" @click="goToSignIn">
    <button class="button">Go to Sign in</button></div>
  </div>
    <h2> {{ status }} </h2>
  </div>
</div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Login',
  data () {
    return {
      form: {
        email: '',
        password: ''
      },
      user: {
        userId: '',
        firstName: '',
        lastName: '',
        email: ''
      },
      authorization: '',
      userId: '',
      status: ''
    }
  },
  methods: {
    goToSignIn () {
      this.$router.push({ name: 'signin' })
    },
    handleSubmit () {
      this.status = 'Loading...'

      var vm = this

      let axiosConfig = {
        headers: {
          'Content-Type': 'application/json',
          'Accept': 'application/json'
        },
        timeout: 1500
      }

      axios.post('https://itec2019rockthecode.herokuapp.com/users/login', this.form, axiosConfig)
        .then(function (response) {
          vm.authorization = response.headers['authorization']
          vm.user.userId = response.headers['userid']
        })
        .catch(function (error) {
          vm.status = error
          console.log(error)
        })
    },
    getUser () {
      var vm = this

      let axiosConfig = {
        headers: {
          'Authorization': vm.authorization,
          'Accept': 'application/json'
        },
        timeout: 1500
      }

      axios.get('https://itec2019rockthecode.herokuapp.com/loginapp/users/' + vm.user.userId, axiosConfig)
        .then(function (response) {
          vm.user = response.data

          vm.status = 'Welcome ' + vm.user.firstName + ' ' + vm.user.lastName + '!'
        })
        .catch(function (error) {
          console.log(error)
        })
    },
    deleteUser () {
      var vm = this

      let axiosConfig = {
        headers: {
          'Authorization': vm.authorization,
          'Accept': 'application/json'
        }
      }

      axios.delete('https://itec2019rockthecode.herokuapp.com/loginapp/users/' + vm.user.userId, axiosConfig)
        .then(function (response) {
          vm.status = 'User deleted'
        })
        .catch(function (error) {
          console.log(error)
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

.toSignIn{
  color: #ee3e52;
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
