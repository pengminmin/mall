<template>
  <el-container class='home-container'>
    <!-- 头部区域 -->
    <el-header>
      <div>
        <img src='../assets/logo.png' alt=''>
        <span>电商后台管理系统</span>
      </div>
      <el-button type='info' @click='logout'>退出</el-button>
    </el-header>
    <!-- 页面主题区域 -->
    <el-container>
      <!-- 侧边栏 -->
      <el-aside :width="isCollapse?'64px':'200px'">
        <div class='toggle-button' @click='toggleCollapse'>|||</div>
        <!-- 侧边栏菜单区域 -->
        <el-menu
          background-color='#333744'
          text-color='#fff'
          active-text-color='#409EFF'
          unique-opened
          :collapse='isCollapse'
          :collapse-transition='false'>
          <!-- 一级菜单 -->
          <el-submenu :index="item.id + ''" v-for='item in menuList' :key='item.id'>
            <!-- 一级菜单的模板区域 -->
            <template slot='title'>
              <i class='el-icon-location'></i>
              <span>{{ item.authName }}</span>
            </template>

            <el-menu-item :index="subItem.id + ''" v-for='subItem in item.children' :key='subItem.id'>
              <template slot='title'>
                <i class='el-icon-menu'></i>
                <span>{{ subItem.authName }}</span>
              </template>
            </el-menu-item>
          </el-submenu>

        </el-menu>
      </el-aside>
      <!-- 右侧内容主体 -->
      <el-main>Main</el-main>
    </el-container>
  </el-container>
</template>

<script>
export default {
  name: 'Home',
  data () {
    return {
      // 左侧菜单数据
      menuList: [
        {
          id: 125,
          authName: '用户管理',
          children: [
            {
              id: 210,
              authName: '用户列表'
            }
          ]
        },
        {
          id: 126,
          authName: '权限管理',
          children: [
            {
              id: 220,
              authName: '角色列表'
            },
            {
              id: 221,
              authName: '权限列表'
            }
          ]
        },
        {
          id: 127,
          authName: '商品管理',
          children: [
            {
              id: 230,
              authName: '商品列表'
            },
            {
              id: 231,
              authName: '分类参数'
            },
            {
              id: 232,
              authName: '商品分类'
            }
          ]
        },
        {
          id: 128,
          authName: '订单管理',
          children: [
            {
              id: 240,
              authName: '订阅列表'
            }
          ]
        },
        {
          id: 129,
          authName: '数据管理',
          children: [
            {
              id: 250,
              authName: '数据列表'
            }
          ]
        }
      ],
      isCollapse: false
    }
  },
  created () {
    this.getMenuList()
  },
  methods: {
    logout () {
      // 清空 token
      window.sessionStorage.clear()
      // 跳转到登录页
      this.$router.push('/login')
    },
    // 获取所有的菜单
    async getMenuList () {
      const { data: res } = await this.$http.get('menus')
      if (res.meta.status !== 200) {
        return this.$message.error(res.meta.msg)
      }
      this.menuList = res.data
    },
    // 点击按钮，切换菜单的折叠与展开
    toggleCollapse () {
      this.isCollapse = !this.isCollapse
    }
  }
}
</script>

<style lang='less' scoped>
.home-container {
  height: 100%;
}

.el-header {
  background-color: #373d41;
  display: flex;
  justify-content: space-between;
  padding-left: 0;
  align-items: center;
  color: #fff;
  font-size: 20px;

  img {
    width: 30px;
    height: 30px;
  }

  > div {
    display: flex;
    align-items: center;

    span {
      margin-left: 15px;
    }
  }
}

.el-aside {
  background-color: #333744;

  .el-menu {
    border-right: none;
  }
}

.el-main {
  background-color: #EAEDF1;
}

.toggle-button {
  background-color: #4A5064;
  font-size: 10px;
  line-height: 24px;
  color: #fff;
  text-align: center;
  letter-spacing: 0.2em;
  cursor: pointer;
}
</style>
