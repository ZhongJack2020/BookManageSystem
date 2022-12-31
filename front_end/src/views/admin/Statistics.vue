<template>
  <div>
    <el-row :gutter="20">
      <el-col :span="6" v-for="item,key in cards" :key="item.title">
        <el-card class="box-card">
          <div slot="header" class="clearfix">{{ item.title }}</div>
          <div class="text item">
            <svg class="icon" aria-hidden="true">
              <use :xlink:href="item.icon" style="width: 100px"></use>
            </svg>
            <span class="text">{{ item.data }}</span>
          </div>
        </el-card>
      </el-col>
    </el-row>
    <div id="myTimer" style="margin-left: 15px; font-weight: 550"></div>
    <!-- 为 ECharts 准备一个具备大小（宽高）的 DOM -->
    <div id="main" style="margin-left: 5px; height: 600px;width: 1000px;"></div>
  </div>
</template>

<script>
import * as echarts from "echarts";
export default {

  data() {
    
    // @TODO 图表数据的位置
    let cards=([
  { title: "已借阅", data: 34, icon: "#iconlend-record-pro" },
  { title: "总访问", data: 58, icon: "#iconvisit" },
  { title: "图书数", data: 400, icon: "#iconbook-pro" },
  { title: "用户数", data: 5, icon: "#iconpopulation" },
]);
    return {
      userName: "",
      userList: [],
      mychart:'',
      cards,

    };
  },
  methods:{
    initCharts:function (){
    this.mychart=echarts.init(document.getElementById("main"));
    this.mychart.setOption({
      title: {
        text: "统计",
      },
      tooltip: {
        trigger: "axis",
        // axisPointer: {
        //   type: 'shadow' // 默认为直线，可选为：'line' | 'shadow'
        // }
      },
      grid: {
        left: "3%",
        right: "4%",
        bottom: "3%",
        containLabel: true,
      },
      xAxis: {
        type: "category",
        data: this.cards.map((item) => item.title),
        axisTick: {
          alignWithLabel: true,
        },
      },
      yAxis: {
        type: "value",
      },
      series: [
        {
          type: "bar",
          label: { show: true },
          barWidth: "25%",
          data: [
            {
              value: this.cards[0].data,
              itemStyle: { color: "#5470c6" },
            },
            {
              value: this.cards[1].data,
              itemStyle: { color: "#91cc75" },
            },
            {
              value:this.cards[2].data,
              itemStyle: { color: "#fac858" },
            },
            {
              value: this.cards[3].data,
              itemStyle: { color: "#ee6666" },
            },
          ],
        },
      ],
    });
    }
  },
  mounted(){
    //this.mychart = echarts.init(document.getElementById("main"));
    this.initCharts();
  }
};
</script>

<style scoped>
.gray-title {
  font-size: 2.2rem;
  color: gray;
  letter-spacing: 1rem;
  text-shadow: 5px 5px 5px gray;
}

.user-table {
  margin-top: 2rem;
  border-radius: 0.5rem;
}

.admin-ctrl {
  display: flex;
  justify-content: space-around;
}
</style>
