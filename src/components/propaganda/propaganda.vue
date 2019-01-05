<template>
  <div class="propaganda">
    <div class="tuiguang">
      <p class="propagandap">推广二维码</p>
      <span>分享二维码赚取更多佣金</span>
      <img class="img" src="../../assets/img/shengl.png" alt>
      <!-- <img src="../../assets/img/erwum.png" alt> -->
      <qriously class="img1" :value="initQCode" :size="180"/>
      <p class="py">邀请码：{{ code }}</p>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      msg: "推广二维码",
      initQCode: "",
      code: ""
    };
  },
  mounted() {
    this.$store.commit("headerTab", true);
    this.$store.commit("footerTab", false);
    this.$store.commit("header", "推广二维码");
    this.$store.commit("fanhui", true);
    this.http.post("/api/create_qrcode").then(res => {
      if (res.code == 200) {
        console.log(res);
        this.initQCode = res.data.data;
        this.code = res.data.code;
      }
    });
  }
};
</script>
<style scoped>
.propaganda {
  padding-top: 0.88rem;
  min-height: 100%;
  background: #f5f5f5;
}
.tuiguang {
  width: 84%;
  height: 7.54rem;
  background: #fff;
  margin: 0 auto;
  margin-top: 0.58rem;
  border-radius: 0.2rem;
  padding-left: 0.3rem;
}
.propagandap {
  padding-top: 0.4rem;
  font-size: 0.36rem;
}
.tuiguang > span {
  display: inline-block;
  padding-top: 0.2rem;
  font-size: 0.24rem;
  padding-bottom: 0.4rem;
}
.img {
  width: 86%;
  margin-left: 4%;
}
.img1 {
  /* width: 41%; */
  text-align: center;
  margin-top: 0.8rem;
}
.py {
  width: 100%;
  text-align: center;
  padding-top: 0.4rem;
}
</style>
