<template>
  <div id="app">
    <div class="container">
      <h1>sign up today</h1>
      <form id="form" @submit="processFormData" ref="form" novalidate>
        <div class="form-group">
          <label for="name">Full name</label>
          <input
            type="text"
            id="name"
            placeholder="Full Name"
            name="name"
            required
            minlength="3"
            maxlength="100"
          />
        </div>

        <div class="form-group">
          <label for="phone">phone Nu,ber</label>
          <input
            type="tel"
            id="phone"
            placeholder="55-555-5555"
            name="phone"
            required
            pattern="[0-9]{3}-[0-9]{3}-[0-9]{4}"
          />
        </div>
        <div class="form-group">
          <label for="email">Email address</label>
          <input type="email" id="email" placeholder="email@address.com" name="email" required />
        </div>
        <div class="form-group">
          <label for="website">Website URl</label>
          <input type="url" id="website" placeholder="http://tikesh.me" name="website" required />
        </div>
        <div class="form-group">
          <label for="password1">Password</label>
          <input
            type="password"
            ref="password1el"
            :style="{'border-color':color}"
            id="password1"
            placeholder="Create Password (Min 8 Characters)"
            required
            pattern="^(?=.*\d)(?=.*[a-z])(?=.*[A-Z])(?=.*[a-zA-Z]).{8,}$"
            title="Please include at least 1 uppercase character, 1 lowercase character ,and 1 number."
          />
        </div>

        <div class="form-group">
          <input
            type="password"
            id="password2"
            ref="password2el"
            :style="{'border-color':color2}"
            placeholder="Confirm Password"
            name="password"
            required
            pattern="^(?=.*\d)(?=.*[a-z])(?=.*[A-Z])(?=.*[a-zA-Z]).{8,}$"
          />
        </div>

        <button type="submit">Registor</button>
      </form>
      <div class="message-container" :style="{'border-color': change2}">
        <h3 id="message" ref="message" :style="{color: change}">{{textContent}}</h3>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      isVAlid: false,
      textContent: "Don't Hesitate!",
      change: "",
      change2: "",
      passwordMatch: false,
      color: "",
      color2: "",
    };
  },

  methods: {
    validateForm() {
      const form = this.$refs["form"];
      const passwoed1el = this.$refs["password1el"];
      const passwoed2el = this.$refs["password2el"];

      //const message= this.$refs['message']
      this.isVAlid = form.checkValidity();
      if (!this.isVAlid) {
        this.textContent = "Please fill out all fields.";
        this.change = "red";
        this.change2 = "red";
        return;
      }
      if (passwoed1el.value === passwoed2el.value) {
        this.passwordMatch = true;
        this.color = "green";
        this.color2 = "green";
      } else {
        this.passwordMatch = false;
        this.textContent = "Make sure passwords match.";
        this.change = "red";
        this.change2 = "red";
        this.color = "red";
        this.color2 = "red";
        return;
      }

      if (this.isVAlid && this.passwordMatch) {
        this.textContent = "Successfully Registored";
        this.change = "green";
        this.change2 = "green";
      }
    },

    storeFormData() {
      const form = this.$refs["form"];
      const user = {
        name: form.name.value,
        phone: form.phone.value,
        email: form.email.value,
        website: form.website.value,
        passwoed: form.password.value,
      };
      console.log(user);
    },

    processFormData(e) {
      e.preventDefault();
      this.validateForm();
      if (this.isVAlid && this.passwordMatch) {
        this.storeFormData();
      }
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Baloo+Tammudu+2&display=swap");
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  min-height: 100vh;
  margin: 0px;
  background: #c9ced3;
  display: flex;
  align-items: center;
  justify-content: center;
  letter-spacing: 2px;
}
.container {
  font-family: "Baloo Tammudu 2", cursive;
  display: flex;
  width: 480px;
  padding-bottom: 10px;
  flex-direction: column;
  align-items: center;
  background: white;
  border-radius: 10px;
  box-shadow: 0 5px 30px 10px rgba(0, 0, 0, 0.4);
}

form {
  width: 90%;
}
.form-group {
  height: 65px;
}
label {
  position: relative;
  bottom: -10px;
  align-self: flex-start;
  display: flex;
}
input {
  width: 100%;
  height: 34px;
  padding: 5px;
  border: 1px solid black;
  border-radius: 5px;
  outline: none;
  box-sizing: border-box;
  transition: all 0.3s;
}
input:valid {
  border: 1px solid green;
}
input:invalid {
  border: 1px solid red;
}
button {
  cursor: pointer;
  color: white;
  background: black;
  border: none;
  border-radius: 5px;
  height: 50px;
  width: 100%;
  font-family: "Baloo Tammudu 2", cursive;
  letter-spacing: 2px;
  margin-top: 15px;
}
button:hover {
  filter: brightness(200%);
  background: rgb(22, 22, 22);
}
button:focus {
  outline: none;
}

.message-container {
  border: 1px solid black;
  border-radius: 5px;
  width: 90%;
  margin-top: 20px;
  display: flex;
  justify-content: center;
  color: black;
}
</style>
