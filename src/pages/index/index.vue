<template>
  <div>
    <el-container>
      <el-aside width="200px">
        <el-menu
          default-active="/index/home"
          router
          class="el-menu-vertical-demo"
          unique-opened
          background-color="#20222A"
          text-color="#fff"
          active-text-color="#ffd04b"
        >
          <el-menu-item index="/index/home">
            <i class="el-icon-menu"></i>
            <span slot="title">首页</span>
          </el-menu-item>


          <div v-for='item in list.menus' :key='item.id'>
          <el-submenu :index="item.url"  v-if="item.children">
            <template slot="title">
              <i class="el-icon-s-custom"></i>
              <span>{{item.title}}</span>
            </template>
            <el-menu-item-group>
              <el-menu-item :index="i.url" v-for='i in item.children' :key='i.id'>{{i.title}}</el-menu-item>
              <!-- <el-menu-item index="/index/role">角色管理</el-menu-item>
              <el-menu-item index="/index/manger">管理员管理</el-menu-item> -->
            </el-menu-item-group>
          </el-submenu>
          <el-menu-item  v-else  :index="item.url">{{item.title}}</el-menu-item>
          </div>
          <!-- <el-submenu index="3">
            <template slot="title">
              <i class="el-icon-s-shop"></i>
              <span>商城管理</span>
            </template>
            <el-menu-item-group>
              <el-menu-item index="/index/classify">商品分类</el-menu-item>
              <el-menu-item index="/index/spec">商品规格</el-menu-item>
              <el-menu-item index="/index/goods">商品管理</el-menu-item>
              <el-menu-item index="/index/vip">会员管理</el-menu-item>
              <el-menu-item index="/index/banner">轮播图管理</el-menu-item>
              <el-menu-item index="/index/seckill">秒杀活动</el-menu-item>
            </el-menu-item-group>
          </el-submenu> -->
        </el-menu>
      </el-aside>
      <el-container>
        <el-header>
          <div class="topBox">
            <div class="boxLeft">{{list.username}}</div>
            <div  class="boxLeft"><el-button type="primary" @click="quit">退出</el-button></div>
          </div>
        </el-header>
        <el-main>
          <el-breadcrumb separator-class="el-icon-arrow-right">
            <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
            <el-breadcrumb-item>{{$route.name}}</el-breadcrumb-item>
          </el-breadcrumb>

          <!-- 二级路由出口 -->
         <div class="login_bottom">
            <router-view></router-view>
         </div>
        </el-main>
      </el-container>
    </el-container>
  </div>
</template>
<script>
import {mapGetters,mapActions} from 'vuex'
export default {
  computed: {
    ...mapGetters({
      list:'user/list'
    })
  },
  components: {},
  data() {
    return {};
  },
  methods: {
    ...mapActions({
      requsetUserLogin:'user/requsetUserLogin'
    }),
    // 退出操作
    quit(){
      // 这是情况sessionStorage
      this.requsetUserLogin({})
      this.$router.push('/login')
    }
  },
  mounted() {
    // this.requsetUserLogin()
 
  },
};
</script>
<style scoped>
.el-header {
  background-color: #b3c0d1;
  color: #333;
  text-align: center;
  line-height: 60px;
}

.el-aside {
  background-color: #20222a;
  color: #333;
  text-align: center;
  line-height: 200px;
  height: 100vh;
}

.el-main {
  background-color: #e9eef3;
  color: #333;
}

.login_bottom{
  margin-top: 20px;
}

/* header区域 */
.topBox{
  float: right;
}
.boxLeft{
  float: left;
}
</style>