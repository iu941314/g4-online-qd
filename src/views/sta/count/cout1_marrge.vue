<template>
  <div style="width: auto;height: 400px" id="main">
  </div>
</template>

<script>
import * as echarts from 'echarts';
export default {
  name: "echarts",
  data() {
    return {
    }
  },
  mounted() {
    this.echartsInit()
  },
  methods:{
    echartsInit() {　　　　　//使用时只需要把setOption里的对象换成echarts中的options或者自己的参数即可
      let echartsEl = document.getElementById('main');
      // 从后端获取数据
      this.getRequest("/g4_count1").then(res =>{
        this.data = res.obj.data;
        console.log("婚姻状况统计");
        console.log(this.data);
        //设置属性
        echarts.init(echartsEl).setOption({  //赋值echarts里面的配置
          title: {
            text: '婚姻状况统计',
            subtext: 'ByG4',
            left: 'center'
          },
          tooltip: {
            trigger: 'item'
          },
          legend: {
            orient: 'vertical',
            left: 'left'
          },
          series: [
            {
              name: '',
              type: 'pie',
              radius: '50%',
              data: this.data,
              emphasis: {
                itemStyle: {
                  shadowBlur: 10,
                  shadowOffsetX: 0,
                  shadowColor: 'rgba(0, 0, 0, 0.5)'
                }
              }
            }
          ]
        })


      })
;

    }
  }
}
</script>
