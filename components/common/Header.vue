<template>
  <el-menu
  :default-active="activeIndex"
  class="el-menu-demo"
  mode="horizontal"
  @select="handleSelect"
  background-color="#545c64"
  text-color="#fff"
  active-text-color="#ffd04b">
  <el-menu-item index="1">
    <nuxt-link to="/">首页</nuxt-link>
  </el-menu-item>
  <el-menu-item index="2">
    <nuxt-link to="/register">注册</nuxt-link>
  </el-menu-item>
</el-menu>
</template>

<script>
export default {
  name: 'Header',
  data () {
    return {
      activeIndex: '1'
    }
  },
  methods: {
    handleSelect (key) {
      this.activeIndex = key
    }
  }
}
</script>

<style>

</style>
