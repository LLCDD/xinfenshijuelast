<template>
  <div class="advertising">
    <p class="advertisingp">
      <span>个人资料</span>
    </p>
    <div class="naph">
      <p class="advertisingp1">
        <span>姓名</span>
        <input type="text" placeholder="输入真实姓名" v-model="username">
      </p>
      <p class="advertisingp1">
        <span>手机号</span>
        <input type="text" placeholder="输入手机号" v-model="phone">
      </p>
    </div>
    <p class="advertisingp" style="margin-top:0.2rem">
      <span>联系地址</span>
    </p>
    <div class="imail">
      <span>详细地址</span>
      <textarea style="margin-top:0.1rem" v-model="text" cols="30" rows="3" placeholder="输入详细地址"></textarea>
    </div>
    <p class="advertisingp" style="margin-top:0.2rem">
      <span>营业执照</span>
    </p>
    <div class="load">
      <p>
        上传执照
        <span>(*可不上传)</span>
        <br>
        <van-uploader class="photo" :after-read="onRead" accept="image/gif, image/jpeg" multiple>
          <van-icon class="icon" name="plus"/>
        </van-uploader>
      </p>
    </div>
    <button @click="load()">确认</button>
  </div>
</template>
<script>
import { Uploader } from "vant";
export default {
  data() {
    return {
      text: "",
      username: "",
      phone: "",
      file: ""
    };
  },
  mounted() {
    this.$store.commit("headerTab", true);
    this.$store.commit("footerTab", false);
    this.$store.commit("header", "广告合作商家");
    this.$store.commit("fanhui", true);
  },
  methods: {
    //   最后的上传事件
    load() {
      const _this = this;
      _this.http
        .post("/api/seller_data", {
          name: _this.username,
          phone: _this.phone,
          mac: _this.text,
          license: _this.file
        })
        .then(res => {
          if (res.code == 200) {
            _this.$toasted.success("操作成功").goAway(1000);
            _this.$router.replace({ name: "personal" });
            // _this.$router.replace({ name: "personal" });
          } else if (res.code == 400) {
            _this.$toasted.error(res.message, { icon: "error" }).goAway(1000);
          }
        })
        .catch(res => {
          _this.$toasted.error(res.message, { icon: "error" }).goAway(1000);
        });
    },
    onRead(file) {
      this.file = file;
    }
  }
};
</script>
<style scoped="">
.advertising {
  padding-top: 0.88rem;
  min-height: 100%;
  background: #f5f5f5;
}
.advertisingp {
  height: 0.8rem;
  width: 100%;
  background: #fff;
  padding-left: 0.3rem;
  padding-top: 0.2rem;
}
.advertisingp > span {
  height: 0.4rem;
  display: inline-block;
  border-left: 3px solid #1e853c;
  padding-left: 0.2rem;
  font-size: 0.3rem;
  color: #1e853c;
  line-height: 0.4rem;
}
.naph {
  margin-top: 0.1rem;
}
.naph > .advertisingp1 {
  height: 0.8rem;
  width: 100%;
  background: #fff;
  padding-left: 0.3rem;
  padding-top: 0.2rem;
}
.naph > .advertisingp1 > span {
  color: #1e853c;
  font-size: 0.3rem;
  display: inline-block;
  width: 1.82rem;
}
.imail {
  padding-left: 0.3rem;
  margin-top: 0.1rem;
  width: 100%;
  background: #fff;
  padding-top: 0.28rem;
}
.imail > span {
  color: #1e853c;

  float: left;
  width: 1.82rem;
  font-size: 0.3rem;
}
.imail > textarea {
  font-size: 0.3rem;
}
.load {
  width: 100%;
  height: 2.34rem;
  background: #fff;
  margin-top: 0.1rem;
  padding-top: 0.3rem;
  padding-left: 0.3rem;
}
.load > p {
  color: #1e853c;
  font-size: 0.3rem;
}
.load > p > span {
  color: #999999;
}
button {
  width: 92%;
  margin-left: 4%;
  margin-top: 0.4rem;
  color: #fff;
  height: 0.8rem;
  border-radius: 0.5rem;
  background: #1e853c;
  font-size: 0.3rem;
}
.photo {
  height: 1.2rem;
  width: 1.2rem;
  text-align: center;
  border: 1px solid #999;

  margin-top: 0.26rem;
  border-radius: 4px;
}
.icon {
  color: #999;
  font-size: 0.7rem;
  line-height: 1.2rem;
}
</style>


