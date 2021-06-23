<template>
  <div class="container">
    <h1 class="label">Login</h1>
    <form class="login_form" method="post" name="loginForm">
      <div class="font"></div>
      <input
        type="text"
        v-model="admin"
        placeholder="Username"
        id="adminUser"
      />
      <div id="user_error">Please fill up your User</div>
      <div class="font font2"></div>
      <input
        type="password"
        v-model="password"
        placeholder="Password"
        id="adminPassword"
        @keyup.enter="loginAction()"
      />
      <div id="pass_error">Please fill up your Password</div>
      <button type="button" @click="loginAction()">Login</button>
      <!--<router-link :to="'About/' + this.admin">
      <i class="as">HELLO</i>
      </router-link>-->
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Home",

  components: {
    
  },

  data() {
    
    return {
      //title: "home",            
      admin: "",
      password: "",
      tokenAuth: ""
    };
  },

  computed: {
    
  },

  created() {
    
  },

  methods: {
    
    loginAction() {
      if (this.admin != "" && this.password != "") {
        // Megnézi, hogy a két login mező ki van e töltve és csak akkor küldi ki a szerverre ha igen.
        const login = { user: this.admin, password: this.password }; 

        console.log(login);
        axios
          .post("https://otthoni-feladat-backend.herokuapp.com/login", login)
          .then((response) => {
            const token = response.data.token;
            //this.tokenAuth = token;
            console.log(token);
            window.location.href = 'Data/';  // Átirányítás a Data-ra
            localStorage.token = token;
            console.log(localStorage.token);
            
          })
          .catch((error) => {
            if (error.response) {
              alert(error.response.data);
            }
          });
      } else {
        console.log("A felhasználó és a jelszó mező kitöltése kötelező");
      }
      this.admin = "";          // Input mezők adatainak törlése.
      this.password = "";
    },
  },
};
</script>

<style scoped>
* {
  padding: 0;
  margin: 0;
}

body {
  background-color: #009879;  
  font-family: sans-serif;
}

.container {
  position: relative;
  margin-top: 130px;
  width: 450px;
  height: auto;
  background: #403d43;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.15);
  border-radius: 8px 8px 8px 8px;
  overflow: hidden;
  margin-left: auto;
  margin-right: auto;
}

h1 {
   text-align: center;
}

.label {
  padding: 20px 130px;
  font-size: 35px;
  font-weight: bold;
  color: #ffffff;
}

.login_form {
  padding: 20px 40px;
}

.login_form .font {
  font-size: 18px;
  color: #ffffff;
  margin: 5px 0;
}

.login_form input {
  height: 40px;
  width: 350px;
  padding: 0 5px;
  font-size: 18px;
  outline: none;
  border: 1px solid silver;
  background: rgb(226, 223, 223);
  border-radius: 5px;
}

.login_form .font2 {
  margin-top: 30px;
}

.login_form button {
  margin: 45px 0 30px 0;
  height: 45px;
  width: 365px;
  font-size: 20px;
  color: white;
  outline: none;
  cursor: pointer;
  font-weight: bold;
  background: #45c2a7;
  border-radius: 5px;
  border: 1px solid #45c2a7;
  transition: 0.5s;
}

.login_form button:hover {
  background: #2d9469;
}

.login_form #user_error,
.login_form #pass_error {
  margin-top: 5px;
  width: 345px;
  font-size: 18px;
  color: #c62828;
  text-align: center;
  padding: 5px 8px;
  border-radius: 3px;
  display: none;
}
</style>
