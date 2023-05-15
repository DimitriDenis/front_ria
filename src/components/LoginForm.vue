
<template>
    <div class="login-container">
      <h1 class="title">Se connecter</h1>
      <form @submit.prevent="login" class="form">
        <div class="form-group">
          <input v-model="user.email" type="email" placeholder="Email" required>
        </div>
        <div class="form-group">
          <input v-model="user.password" type="password" placeholder="Mot de passe" required>
        </div>
        <button type="submit" class="btn">Se connecter</button>
        <p class="error">{{ error }}</p>
      </form>
    </div>
  </template>
  
  <script>
  import axios from '../axios/axios.js';
  export default {
    data() {
      return {
       user: {
        email: "",
        password: "",
       },
        error: "",
      };
    },
    methods: {
      async login() {
        this.error = "";
        try {
          
          const response = await axios.post("/api/login", this.user);
          localStorage.setItem("user", JSON.stringify(response.data.user));
          localStorage.setItem("token", response.data.token);
          this.$router.push({ name: "Dashboard" });
        } catch (err) {
          this.error = "Email ou mot de passe invalide.";
          //console.error(err?.config);
        }
      },
    },
  };
  </script>
  
  <style scoped>
  .login-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: 20px;
  }
  
  .title {
    font-size: 30px;
    margin-bottom: 20px;
  }
  
  .form {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  
 
  </style>
