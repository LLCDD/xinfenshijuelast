<template>
  <div class="div">
    <mt-swipe :auto="4000" style="width:100%;height:3.78rem">
      <mt-swipe-item v-for="(item,index) in list" :key="index">
        <img style="height:100%;width:100%" :src="url +'/'+ item" alt>
      </mt-swipe-item>
    </mt-swipe>
    <div class="nr">
      <span class="xie">
        <img src="../../assets/img/header.png" alt>
      </span>
      <div class="nr1">
        <p>234234</p>
        <p>23423432</p>
      </div>
    </div>
    <div class="event">
      <router-link tag="span" to="/whypropaganda">
        <img src="../../assets/img/01.png" alt>
        <span>如何宣传</span>
      </router-link>
      <router-link tag="span" to="/vip">
        <img src="../../assets/img/2.png" alt>
        <span>鑫峰会员</span>
      </router-link>
      <router-link tag="span" to="/propaganda">
        <img src="../../assets/img/3.png" alt>
        <span>推广二维码</span>
      </router-link>
      <router-link tag="span" to="/outer">
        <img src="../../assets/img/6.png" alt>
        <span>关于我们</span>
      </router-link>
    </div>
    <van-popup v-model="show" class="toast">
      <div class="toaste">公告信息</div>
      <div class="div5"></div>
      <div class="toaste" @click="toasts">我知道了</div>
    </van-popup>
  </div>
</template>
<script>
import { Toast } from "vant";
import { Popup } from "vant";
export default {
  data() {
    return {
      msg: "首页",
      show: false,
      list: JSON.parse(localStorage.getItem("img")),
      url: localStorage.getItem("url")
    };
  },
  mounted() {
    this.$store.commit("headerTab", true);
    this.$store.commit("footerTab", true);
    this.$store.commit("header", "鑫峰视觉");
    this.$store.commit("fanhui", false);
    Toast.clear();

    if (localStorage.getItem("toast") <= 1) {
      this.show = true;
      localStorage.setItem("toast", 3);
    } else {
      this.show = false;
    }
    // JSON.stringify
    // JSON.parse;
    console.log(JSON.parse(localStorage.getItem("img")));
    // console.log(localStorage.getItem("token"));
  },
  methods: {
    toasts() {
      this.show = false;
    }
  }
};
</script>
<style scope="">
.div {
  min-height: 100%;
  background: #f5f5f5;
  padding-top: 0.88rem;
}
.nr {
  width: 100%;
  height: 1.2rem;
  background: #fff;
  padding: 0.2rem 0;
  padding-left: 0.3rem;
}
.xie {
  font-size: 0.36rem;
  color: #1e853c;
  font-style: italic;
  font-weight: 700;
  display: inline-block;
  width: 12%;
  line-height: 0.4rem;
  /* margin-right: 0.34rem; */
}
.nr1 {
  /* display: inline-block; */
  height: 100%;
  float: right;
  width: 82%;
  padding-left: 0.3rem;
  margin-left: 0.34rem;
  border-left: 2px solid #1e853c;
}
.nr1 > p {
  line-height: 0.36rem;
  font-size: 0.24rem;
}
.event {
  margin-top: 0.2rem;
  width: 100%;
  height: 3.22rem;
  background: #fff;
}
.event > span {
  display: inline-block;
  width: 50%;
  height: 50%;
  border-right: 2px solid #f5f5f5;
  border-bottom: 2px solid #f5f5f5;
  padding-top: 0.32rem;
  padding-left: 0.6rem;
}
.event > span > img {
  height: 1rem;
  width: 1rem;
}
.event > span > span {
  margin-left: 0.22rem;
  font-size: 0.26rem;
}
.xie > img {
  height: 100%;
  width: 100%;
}
.toast {
  background: #e6e6e6;
  height: 84%;
  width: 80%;
  border-radius: 6px;
  overflow: hidden;
}
.toaste {
  height: 8%;
  background: #1e853c;
  font-size: 0.34rem;
  color: #fff;
  text-align: center;
  line-height: 0.88rem;
}
.div5 {
  height: 84%;
  color: #333333;
}
</style>
