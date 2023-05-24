<template>
  <div style="width: auto;height: 400px" id="main2">
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
      let echartsEl = document.getElementById('main2');
      // 从后端获取数据
      this.getRequest("/g4_countSex").then(res =>{
        //获取数据
        this.data = res.obj.data;
        console.log(this.data);
        echarts.init(echartsEl).setOption( {
          title: {
            text: '男女比例',
            left: 'center',
            top: 0,

          },
          tooltip: {
            trigger: 'item'
          },
          legend: {
            top: '5%',
            left: 'center'
          },
          series: [
            {
              name: 'by G4',
              type: 'pie',
              radius: ['40%', '70%'],
              avoidLabelOverlap: false,
              itemStyle: {
                borderRadius: 10,
                borderColor: '#fff',
                borderWidth: 2
              },
              label: {
                show: false,
                position: 'center'
              },
              emphasis: {
                label: {
                  show: true,
                  fontSize: 40,
                  fontWeight: 'bold'
                }
              },
              labelLine: {
                show: false
              },
              data:this.data
            }
          ]
        })


      })
;

    }
  }
}
</script>
