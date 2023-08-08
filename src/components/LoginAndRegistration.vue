<script setup>
    import { ref, reactive, computed } from 'vue'
    const formDisplay = ref(false)

    function changeformDisplay(){
        if(formDisplay.value==true){
            formDisplay.value = false;
        }else{
            formDisplay.value = true;
        }
    }

    const previousLoginData = reactive({username: 'sajid', password: '123'})

    function changeLoginSubmit() {
    const name = previousLoginData.name
    const pass = previousLoginData.pass
    if (name === previousLoginData.username && pass === previousLoginData.password) {
        return 'Login Successful'
    } else {
        loginError = true
        return 'Login Information was Wrong!'
    }
}

</script>

<template>

<div class="container">
    <div class="form-container" id="login-form" v-if="false==formDisplay">
        <h1>Login</h1>
        <div class="alert alert-danger" role="alert">
            {{ changeLoginSubmit() }}
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
            <!-- <div class="alert alert-primary" role="alert" v-show="previousLoginData.username==previousLoginData.name && previousLoginData.password==previousLoginData.pass">
                A simple primary alert—check it out!
            </div> -->
        <form>
            <label for="new-username">Username</label>
            <input type="text" id="new-username" name="new-username" required>
            <label for="new-email">Email</label>
            <input type="email" id="new-email" name="new-email" required>
            <label for="new-password">Password</label>
            <input type="password" id="new-password" name="new-password" required>
            <button type="submit">Sign Up</button>
        </form>
        <p>Already have an account? <a href="#" id="login-link" @click="changeformDisplay()">Login</a></p>
    </div>
  </div>

</template>
<style scoped>
    .container {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
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