<template>
  <div>
    <!-- 面包屑导航区域 -->
    <el-breadcrumb separator='/'>
      <el-breadcrumb-item :to="{ path: '/home' }">首页</el-breadcrumb-item>
      <el-breadcrumb-item>用户管理</el-breadcrumb-item>
      <el-breadcrumb-item>用户列表</el-breadcrumb-item>
    </el-breadcrumb>

    <!-- 卡片试图区域 -->
    <el-card>
      <!-- 搜索和添加区域 -->
      <el-row :gutter='10'>
        <el-col :span='8'>
        <el-input placeholder='请输入内容'>
          <el-button slot='append' icon='el-icon-search'></el-button>
        </el-input>
        </el-col>
        <el-col :span='4'>
        <el-button type='primary'>添加用户</el-button>
        </el-col>
      </el-row>
    </el-card>
  </div>
</template>

<script>
export default {
  name: 'Users'
}
</script>

<style scoped>

</style>
