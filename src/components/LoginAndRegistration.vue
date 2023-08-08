<script setup>
    import { ref, reactive, computed } from 'vue'
    const formDisplay = ref(false)
    const formCodeClear = ref(false)

    function changeformDisplay(){
        if(formDisplay.value==true){
            formDisplay.value = false;
        }else{
            formDisplay.value = true;
        }
    }

    const previousLoginData = reactive({username: '', password: '', status: true})

    function logout(){
      formCodeClear.value = false
    }

    function changeLoginSubmit() {
      if (previousLoginData.name==previousLoginData.username && previousLoginData.pass==previousLoginData.password) {
        previousLoginData.status = true
        formCodeClear.value = true
      } else {
        previousLoginData.status = false
        formCodeClear.value = false
      }
    }

    const userRegistrationData = reactive({newUsername: '', newPassword: '', confirmPassword: '', status: false})

    function registrationDataSubmit(){
      if (userRegistrationData.confirmPassword == userRegistrationData.newPassword) {
        userRegistrationData.status = true

        previousLoginData.username = userRegistrationData.newUsername
        previousLoginData.password = userRegistrationData.newPassword
        previousLoginData.status = true
      }else {
        userRegistrationData.status = false

        previousLoginData.username = ''
        previousLoginData.password = ''
        previousLoginData.status = false
      }
    }


    // QNA SCRIPT START

    const saarcCountries = reactive([
      { name: "Bangladesh", capital: "Dhaka" },
      { name: "Nepal", capital: "Kathmandu" },
      { name: "Bhutan", capital: "Thimphu" },
      { name: "Sri Lanka", capital: "Colombo" },
      { name: "India", capital: "New Delhi" },
      { name: "Pakistan", capital: "Islamabad" },
      { name: "Maldives", capital: "Male" }
    ])

    const capitals = ["Dhaka", "Kathmandu", "Thimphu", "Colombo", "New Delhi", "Islamabad", "Male"]

    function getScore(){
        let score = 0
        saarcCountries.forEach(country => {
            if(country.answer == country.capital){
                score++
            }
        })
        return score
    }

    const displayScore = ref(false)
    function getResult(){
      displayScore.value = true
    }

</script>

<template>

<div class="container" style="padding: 100px 0;" v-if="false==formCodeClear">
  <div class="form-container" id="login-form" v-if="false==formDisplay">
      <h1>Login</h1>
      <div class="alert alert-danger" role="alert" v-if="false==previousLoginData.status">
          Login Information was Wrong
      </div>
      <form @submit.prevent="changeLoginSubmit()">
          <label for="username">Username</label>
          <input type="text" id="username" name="username" v-model="previousLoginData.name" required>
          <label for="password">Password</label>
          <input type="password" id="password" name="password" v-model="previousLoginData.pass" required>
          <button type="submit">Login</button>
      </form>
      <p>Don't have an account? <a href="#" id="signup-link" @click="changeformDisplay()">Sign up</a></p>
  </div>

  <div class="form-container" id="signup-form" v-if="true==formDisplay">
      <h1>Sign Up</h1>
          <div class="alert alert-primary" role="alert" v-show="true === userRegistrationData.status">
              Registration Successful <a href="#" @click="changeformDisplay()">Login</a>
          </div>
      <form @submit.prevent="registrationDataSubmit()">
          <label for="new-username">Username</label>
          <input type="text" id="new-username" name="newUsername" v-model="userRegistrationData.newUsername" required>
          <label for="new-password">Password</label>
          <input type="password" id="password" name="newPassword" v-model="userRegistrationData.newPassword" required>
          <label for="new-password">Confirm Password</label>
          <input type="password" id="confirm-password" name="confirmPassword" v-model="userRegistrationData.confirmPassword" required>
          <button type="submit">Sign Up</button>
      </form>
      <p>Already have an account? <a href="#" id="login-link" @click="changeformDisplay()">Login</a></p>
  </div>

</div>

<div class="container" v-if="true==formCodeClear">
  <div class="row py-5">
    <div class="col-sm-12">
      <div class="card text-start">
        <div class="card-body text-center">
          <h2 class="text-center">QNA</h2>

                <div class="my-2 border border-gray-400 p-3" v-for="country in saarcCountries">
                    <p>What is the capital of {{ country.name }} ?</p>
                    <template v-for="capital in capitals" :key="index">
                        <input type="radio" :value="capital" v-model="country.answer"/>
                        <label class="ml-2 mx-2">{{ capital }}</label>
                    </template>
                </div>
                <div class="d-grid gap-2 col-6 mx-auto">
                    <h3 class="text-primary my-3" v-show="true==displayScore">Your Score: {{ getScore() }} out of 7</h3>
                    <button class="btn btn-warning mt-2 mb-5" @click="getResult()">Get Result</button>
                </div>
          <button class="text-center" @click="logout()">LogOut</button>
        </div>
      </div>
    </div>
  </div>
</div>

</template>
<style scoped>
  #qna {
    background-color: #000;
  }
    .container {
      display: flex;
      justify-content: center;
      align-items: center;
      height: auto;
      /* height: 100vh; */
    }

    .form-container {
      width: 600px;
      margin: 0 auto;
      padding: 50px;
      background-color: #333;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
      color: #fff;
    }

    h1 {
      text-align: center;
      margin-bottom: 30px;
      font-size: 36px;
      color: #b38bff;
    }

    form {
      display: flex;
      flex-direction: column;
    }

    label {
      margin-bottom: 10px;
      font-size: 18px;
    }

    input {
      padding: 12px;
      border: none;
      border-radius: 5px;
      margin-bottom: 20px;
      font-size: 16px;
      color: #fff;
      background-color: #555;
    }

    button {
      padding: 10px;
      background-color: #b38bff;
      color: #fff;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      font-size: 18px;
      transition: background-color 0.2s ease-in-out;
    }

    button:hover {
      background-color: #8c5fb2;
    }

    a {
      text-decoration: none;
      color: #b38bff;
      font-size: 18px;
      transition: color 0.2s ease-in-out;
    }

    a:hover {
      color: #8c5fb2;
    }

    p {
      text-align: center;
      margin: 8px;
    }
</style>