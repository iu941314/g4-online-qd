<template>
  <div class="chart-container">

    <el-tabs v-model="activeName" type="card">

      <el-tab-pane label="男女比例" name="Sex">
        <div v-if="'Sex' === activeName">
          <Sex/>
        </div>
      </el-tab-pane>

      <el-tab-pane label="婚姻状况" name="Marriage">
        <div v-if="'Marriage' === activeName">
          <Marriage/>
        </div>
      </el-tab-pane>

      <el-tab-pane label="学历统计" name="Edu">
        <div v-if="'Edu' === activeName">
          <Edu/>
        </div>
      </el-tab-pane>

      <el-tab-pane label="部门人员比例" name="DePartment">
        <div v-if="'DePartment' === activeName">
          <DePartment/>
        </div>
      </el-tab-pane>

      <el-tab-pane label="员工分布图" name="MapChina">
        <div v-if="'MapChina' === activeName">
          <MapChina/>
        </div>
      </el-tab-pane>

    </el-tabs>


    <!--踩坑  https://blog.csdn.net/m0_38039437/article/details/128565602-->


  </div>


</template>

<script>

import Marriage from "./count/cout1_marrge.vue";
import DePartment from "./count/cout2_department.vue";
import Sex from "./count/cout3_Sex.vue";
import Edu from "./count/cout4_educationbackground.vue"
import MapChina from "./count/cout5_personnelDistribution.vue"

export default {
  data() {
    return {
      activeName: 'MapChina'
    }
  },
  components: {
    Marriage,
    DePartment,
    Sex,
    Edu,
    MapChina,
  }
}
</script>


<style scoped>


</style>
