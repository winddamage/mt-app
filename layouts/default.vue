<template>
  <el-container>
    <el-header>
      <header-com></header-com>
    </el-header>
    <el-main>
      <nuxt />
    </el-main>
    <el-footer></el-footer>
  </el-container>
</template>

<script>
import HeaderCom from '~/components/common/Header.vue'
export default {
  components: {
    HeaderCom
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
html {
  font-family: 'Source Sans Pro', -apple-system, BlinkMacSystemFont, 'Segoe UI',
    Roboto, 'Helvetica Neue', Arial, sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}
</style>
