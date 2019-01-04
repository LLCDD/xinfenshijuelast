<template>
  <div class="addcard">
    <div>
      <span>原密码</span>
      <input type="password" placeholder="输入原密码" v-model="oldpassword">
    </div>
    <div>
      <span>新密码</span>
      <input type="password" placeholder="输入新密码" v-model="password">
    </div>
    <div>
      <span>重复新密码</span>
      <input type="password" placeholder="重复输入新密码" v-model="password1">
    </div>
    <button @click="add()">确认修改</button>
  </div>
</template>
<script>
export default {
  data() {
    return {
      password1: "",
      oldpassword: "",
      password: ""
    };
  },
  mounted() {
    this.$store.commit("headerTab", true);
    this.$store.commit("footerTab", false);
    this.$store.commit("header", "修改密码");
    this.$store.commit("fanhui", true);
  },
  methods: {
    add() {
      console.log("修改成功");
      this.$router.replace({ name: "login" });
    }
  }
};
</script>
<style scoped>
.addcard {
  padding-top: 0.88rem;
  min-height: 100%;
  background: #f5f5f5;
}
.addcard > div {
  width: 100%;
  background: #fff;
  height: 0.82rem;
  border-bottom: 2px solid #f5f5f5;
  line-height: 0.8rem;
  padding-left: 0.3rem;
}
.addcard > div > span {
  font-size: 0.3rem;
  color: #1e853c;
  display: inline-block;
  width: 1.8rem;
}
.addcard > div > input {
  font-size: 0.3rem;
}
button {
  width: 86%;
  height: 0.8rem;
  background: #1e853c;
  border-radius: 0.5rem;
  margin-left: 7%;
  margin-top: 0.52rem;
  color: #fff;
}
.addcard > div > input {
  height: 90%;
}
</style>
