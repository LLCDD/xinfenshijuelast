<template>
  <div class="static">
    <table class="table">
      <tr style="height:0.8rem">
        <th class="thc">时间</th>
        <th class="thc">金额</th>
        <th class="thc">操作</th>
      </tr>
      <tr style="height:0.8rem;border:0" v-for="(item,index) in list" :key="index">
        <td style="color:#999">{{ item.timer }}</td>
        <td style="color:#000">{{ item.money }}</td>
        <td style="color:#000">{{ item.state }}</td>
      </tr>
    </table>
  </div>
</template>
<script>
import { Toast } from "vant";
export default {
  data() {
    return {
      list: [
        {
          timer: "2018/12/20 14:40:00",
          money: "100",
          state: "1"
        },
        {
          timer: "2018/12/20 14:40:00",
          money: "100",
          state: "2"
        },
        {
          timer: "2018/12/20 14:40:00",
          money: "100",
          state: "0"
        }
      ]
    };
  },
  beforeCreate() {
    Toast.loading({
      mask: true,
      message: "加载中..."
    });
  },
  mounted() {
    this.$store.commit("headerTab", true);
    this.$store.commit("footerTab", false);
    this.$store.commit("header", "静态收益记录");
    this.$store.commit("fanhui", true);
    this.http
      .post("/api/profit", { type: 1 })
      .then(res => {
        if (res.code == 200) {
          this.list = res.data.data;
          Toast.clear();
        } else if (res.code == 400) {
          this.$toasted.error(res.message, { icon: "error" }).goAway(1000);
        }
      })
      .catch(res => {
        this.$toasted.error(res.message, { icon: "error" }).goAway(1000);
      });
  }
};
</script>
<style scoped>
.static {
  padding-top: 0.88rem;
}
.table {
  margin-top: 0.1rem;
  background: #fff;
  width: 100%;
}
.thc {
  color: #1e853c;
  font-size: 0.3rem;
}
table {
  border: 0;
}
th {
  border: 0;
  border-bottom: 2px solid #f5f5f5;
}
td {
  border: 0;
  border-bottom: 2px solid #f5f5f5;
}
</style>
