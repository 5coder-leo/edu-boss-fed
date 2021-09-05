<template>
  <el-container>
    <el-aside width="200px">
      <app-aside/>
    </el-aside>
    <el-container>
      <el-header>
        <app-header/>
      </el-header>
      <el-main>
        <router-view/>
      </el-main>
    </el-container>
  </el-container>
</template>

<script lang="ts">
import Vue from 'vue'
import AppAside from './component/app-aside.vue'
import AppHeader from './component/app-header.vue'

export default Vue.extend({
  name: 'LayoutIndex',
  components: {
    AppAside,
    AppHeader
  }
})
</script>

<style scoped lang="scss">
.el-container {
  min-height: 100vh;
  min-width: 980px;
}

.el-aside {
  background-color: #d3dce6;
}

.el-header {
  background-color: #fff;
}

.el-main {
  background-color: #e9eef3;
}
</style>
