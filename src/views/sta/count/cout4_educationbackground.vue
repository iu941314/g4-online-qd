<template>
  <div style="width: auto;height: 400px" id="main3">
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
    echartsInit() {　

      　　　　//使用时只需要把setOption里的对象换成echarts中的options或者自己的参数即可
      let echartsEl = document.getElementById('main3');
      // 从后端获取数据
      this.getRequest("/g4_countEdu").then(res =>{
        console.log(res.obj);
        //获取数据
        this.data = res.obj;

        echarts.init(echartsEl).setOption(
             {
               title: {
                 text: '学历统计',
                 subtext: 'by G4',
                 left: 'center',
                 top: 0,
               },
              xAxis: {
                type: 'category',
                data:this.data.xAxis,
              },
              yAxis: {
                type: 'value'
              },
              series: [
                {
                  data: this.data.yAxis,
                  type: 'bar',
                  showBackground: true,
                  backgroundStyle: {
                    color: 'rgba(180, 180, 180, 0.2)'
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
