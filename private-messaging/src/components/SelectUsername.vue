<template>
  <div class="login-page">
    <div class = "form">
      <div class="imgcontainer">
        <img src="../../../../images/avatar.png" alt="Avatar" class="avatar">
      </div>
    <form @submit.prevent="onSubmit">
      <input v-model="username" placeholder="Your username..." />
      <button :disabled="!isValid">Send</button>
    </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "SelectUsername",
  data() {
    return {
      username: "",
    };
  },
  computed: {
    isValid() {
      return this.username.length > 2;
    },
  },
  methods: {
    onSubmit() {
      this.$emit("input", this.username);
    },
  },
};
</script>

<style scoped>
.login-page {
  width: 360px;
  padding: 8% 0 0;
  margin: auto;
  font-family:Verdana, Geneva, Tahoma, sans-serif;
}

.imgcontainer {
  text-align: center;
  margin: 0 0 24px 0;
}
img.avatar {
  width: 60%;
  border-radius: 50%;
}

.form {
  position: relative;
  z-index: 1;
  background: #FFFFFF;
  max-width: 360px;
  margin: 0 auto 100px;
  padding: 45px;
  text-align: center;
  box-shadow: 0 0 20px 0 rgba(0, 0, 0, 0.2), 0 5px 5px 0 rgba(0, 0, 0, 0.24);
}

.form input {
  font-family:Verdana, Geneva, Tahoma, sans-serif;
  outline: 0;
  background: #f2f2f2;
  width: 100%;
  border: 0;
  margin: 0 0 15px;
  padding: 15px;
  box-sizing: border-box;
  font-size: 14px;
}
.form button {
  font-family: "Roboto", sans-serif;
  text-transform: uppercase;
  outline: 0;
  background: #8cc4ec;
  width: 100%;
  border: 0;
  padding: 15px;
  color: #FFFFFF;
  font-size: 14px;
  -webkit-transition: all 0.3 ease;
  transition: all 0.3 ease;
  cursor: pointer;
}

.form button:hover,.form button:active,.form button:focus {
  background: #6bb4e7;
}

</style>
