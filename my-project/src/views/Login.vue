<template>
  <div>
    <form v-if="!isSign">
      <div>用户名：</div>
      <input type="text" v-model="name">
      <div>密码：</div>
      <input type="password" v-model="password">
      <button type="button" @click="login()">登录</button>
      <button type="button" @click="sign()">注册</button>
    </form>
    <form v-else>
      <div>用户名：</div>
      <input type="text" v-model="name">
      <div>密码：</div>
      <input type="password" v-model="password">
      <div>确认密码：</div>
      <input type="password" v-model="repeat">
      <button type="button" @click="addUser()">确定</button>
      <button type="button" @click="cancel()">取消</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "Login",
  data() {
    return {
      isSign: false,
      name: "",
      password: "",
      repeat: ""
    };
  },
  methods: {
    login() {
      let localName = localStorage.getItem("name");
      let localPassword = localStorage.getItem("password");
      if (this.name === localName && this.password === localPassword) {
        this.name = "";
        this.password = "";
        this.$router.push("/Home/list");
        alert("登录成功");
      } else {
        alert("用户名或密码不正确");
      }
    },
    sign() {
      this.isSign = true;
    },
    addUser() {
      if (this.password === this.repeat) {
        localStorage.setItem("name", this.name);
        localStorage.setItem("password", this.password);
        alert("注册成功");
        this.name = "";
        this.password = "";
        this.repeat = "";
        this.isSign = false;
      } else {
        alert("两次密码输入不正确");
        this.repeat = "";
      }
    },
    cancel() {
      this.isSign = false;
    }
  }
};
</script>

<style scoped>
</style>
