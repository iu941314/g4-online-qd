<template>
  <div style="width: auto ;height: 650px;background-color: #dbf4fc" id="main41">
  </div>
</template>

<script>
import * as echarts from 'echarts';
import china from "@/assets/china.json" //引入地图json
echarts.registerMap('china',china);// 用json注册中国地图
export default {
  name: "echarts",
  data() {
    return {}
  },
  mounted() {
    this.echartsInit()
  },
  methods: {
    echartsInit() {
      //使用时只需要把setOption里的对象换成echarts中的options或者自己的参数即可
      let echartsEl = document.getElementById('main41');
      // 从后端获取数据
      this.getRequest("/g4_countProvice").then(res => {
        // console.log(res.obj.data);
        // //获取数据
        // // this.data = res.obj.data;
        // 数据============================
        var mapData =  res.obj.data;

        // 数据============================

        // 图表
        echarts.init(echartsEl).setOption( {
          title: {
            text: "公司员工籍贯分布图",
            left: "center",
          },
          tooltip: {
            trigger: "item",
          },
          legend: {
            orient: "vertical",
            left: "left",
            data: ["公司员工籍贯分布图"],
          },
          visualMap: {
            type: "piecewise",
            pieces: [{
              min: 21,
              max: 500,
              label: ">20",
              color: "#00688B",
            },
              {
                min: 16,
                max: 20,
                label: "16-20人",
                color: "#87CEFF"
              },
              {
                min: 11,
                max: 15,
                label: "10-15人",
                color: "#7EC0EE"
              },
              {
                min: 6,
                max: 10,
                label: "6-10",
                color: "#6CA6CD"
              },
              {
                min: 1,
                max: 5,
                label: "1-5人",
                color: "#C6E2FF"
              },
              {
                min: 0,
                max: 0,
                label: "0人",
                color: "red"
              }
            ],
            color: ["#E0022B", "#E09107", "#A3E00B"],
          },
          toolbox: {
            show: true,
            orient: "vertical",
            left: "right",
            top: "center",
            feature: {
              mark: {
                show: true
              },
              dataView: {
                show: true,
                readOnly: false
              },
              restore: {
                show: true
              },
              saveAsImage: {
                show: true
              },
            },
          },
          roamController: {
            show: true,
            left: "right",

          },

          geo: {
            //地理坐标系组件用于地图的绘制
            map: "china",
            roam: false, //不开启缩放和平移
            label: {
              normal: {
                show: true,
                fontSize: "10",
                color: "rgba(0,0,0,0.7)",
              },
            },
            itemStyle: {
              normal: {
                color: 'rgba(51, 69, 89, .5)', //地图背景色
                borderColor: '#516a89', //省市边界线00fcff 516a89
                borderWidth: 1,
              },
              emphasis: {
                areaColor: "#1DE9B6", //鼠标选择区域颜色
                shadowOffsetX: 0,
                shadowOffsetY: 0,
                shadowBlur: 20,
                borderWidth: 0,
                shadowColor: "rgba(0, 0, 0, 0.5)",
              },
            },
          },
          series: [{
            name: "人口数",
            type: "map", //图表类型
            geoIndex: 0,
            data: mapData, //图表的数据
          },
          ],
          color: '#f5f5f5'
        })

      })
    }
  }
}
</script>
