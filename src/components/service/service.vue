<template>
  <div class="service">
    <p class="service1">
      <span>客服1</span>
    </p>
    <p class="servicephone">
      <span>手机号</span>
      {{ phone }}
    </p>
    <p class="servicewx">
      <span>微信号</span>
      {{ wx }}
    </p>
    <p class="service2">
      <span>客服1</span>
    </p>
    <p class="servicephone">
      <span>手机号</span>
      {{ phone1 }}
    </p>
    <p class="servicewx">
      <span>微信号</span>
      {{ wx }}
    </p>
  </div>
</template>
<script>
import { Toast } from "vant";
export default {
  data() {
    return {
      msg: "客服中心",
      phone: "",
      wx: "",
      phone1: "",
      wx1: ""
    };
  },
  beforeCreate() {
    Toast.loading({
      mask: true,
      message: "加载中...",
      duration: "100000"
    });
  },
  mounted() {
    this.$store.commit("headerTab", true);
    this.$store.commit("footerTab", false);
    this.$store.commit("header", "客服中心");
    this.$store.commit("fanhui", true);
    this.http.post("/api/servertel_list").then(res => {
      if (res.code == 200) {
        Toast.clear();
        this.phone = res.data.data[0].tel;
        this.wx = res.data.data[0].wechatno;
        this.phone1 = res.data.data[1].tel;
        this.wx1 = res.data.data[1].wechatno;
        console.log(res);
      }
    });
  }
};
</script>
<style scoped>
.service {
  min-height: 100%;
  padding-top: 0.88rem;
  background: #f5f5f5;
}
.service1 {
  width: 100%;
  color: #1e853c;
  height: 0.8rem;
  padding-left: 0.3rem;
  background: #fff;
}
.service1 > span {
  font-size: 0.3rem;
  padding-left: 0.18rem;
  border-left: 4px solid #1e853c;
  line-height: 0.8rem;
  height: 0.4rem;
}
.servicephone {
  width: 100%;
  background: #fff;
  margin-top: 0.2rem;
  height: 0.8rem;
  color: #1e853c;
  font-size: 0.3rem;
  border-bottom: 2px solid #f5f5f5;
}
.servicephone > span {
  display: inline-block;
  padding-left: 0.3rem;
  line-height: 0.8rem;
  width: 1.82rem;
}
.servicewx {
  width: 100%;
  background: #fff;
  height: 0.8rem;
  color: #1e853c;
  font-size: 0.3rem;
}
.servicewx > span {
  display: inline-block;
  padding-left: 0.3rem;
  line-height: 0.8rem;
  width: 1.82rem;
}
.service2 {
  width: 100%;
  color: #1e853c;
  height: 0.8rem;
  padding-left: 0.3rem;
  background: #fff;
  margin-top: 0.2rem;
}
.service2 > span {
  font-size: 0.3rem;
  padding-left: 0.18rem;
  border-left: 4px solid #1e853c;
  line-height: 0.8rem;
  height: 0.4rem;
}
</style>
