<template>
  <div class="nav-father">
    <div class="navbar">
      <hamburger :is-active="sidebar.opened" class="hamburger-container" @toggleClick="toggleSideBar" />
      <selectrouter class="hamburger-container"  @toggleMenu='firstMenu'/>
      <breadcrumb class="breadcrumb-container" />
      <div class="right-menu">
        <el-dropdown class="avatar-container" trigger="click">
          <div class="avatar-wrapper">
            <img :src="avatar+'?imageView2/1/w/80/h/80'" class="user-avatar">
            <i class="el-icon-caret-bottom" />
          </div>
          <el-dropdown-menu slot="dropdown" class="user-dropdown">
            <router-link to="/">
              <el-dropdown-item>
                Home
              </el-dropdown-item>
            </router-link>
            <a target="_blank" href="https://github.com/PanJiaChen/vue-admin-template/">
              <el-dropdown-item>Github</el-dropdown-item>
            </a>
            <a target="_blank" href="https://panjiachen.github.io/vue-element-admin-site/#/">
              <el-dropdown-item>Docs</el-dropdown-item>
            </a>
            <el-dropdown-item divided>
              <span style="display:block;" @click="logout">Log Out</span>
            </el-dropdown-item>
          </el-dropdown-menu>
        </el-dropdown>
      </div>
    </div>
    <div v-show="firstMenuPannel" class="first-menu-pannel">
      <i class="el-icon-caret-top"></i>
      <div class="first-menu-table">
        <el-row :gutter="10">
          <el-col :span="8"  v-for="route in menuRoutes" :key="route.path" :item="route">
            <router-link :to="route.path">
            <div class="grid-content bg-purple">
              {{route.name}}
            </div>
            </router-link>
          </el-col>
        </el-row>
      </div>
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import Breadcrumb from '@/components/Breadcrumb'
import Hamburger from '@/components/Hamburger'
import Selectrouter from '@/components/selectRouter'

export default {
  components: {
    Breadcrumb,
    Hamburger,
    Selectrouter
  },
  data(){
    return{
      firstMenuPannel:false
    }
  },
  computed: {
    ...mapGetters([
      'sidebar',
      'avatar'
    ]),
    menuRoutes(){
      // this.$router.options.routes.filter((item)=>{
      //   if(item.hidden) return item
      // })
      return this.$router.options.routes
    }

  },
  methods: {
    toggleSideBar() {
      this.$store.dispatch('app/toggleSideBar')
    },
    async logout() {
      await this.$store.dispatch('user/logout')
      this.$router.push(`/login?redirect=${this.$route.fullPath}`)
    },
    firstMenu(data){
      this.firstMenuPannel=data
    }
  }
}
</script>

<style lang="scss" scoped>
.nav-father{
  position: relative;
}
.navbar {
  height: 50px;
  overflow: hidden;
  position: relative;
  background: #fff;
  box-shadow: 0 1px 4px rgba(0,21,41,.08);

  .hamburger-container {
    line-height: 46px;
    height: 100%;
    float: left;
    cursor: pointer;
    transition: background .3s;
    -webkit-tap-highlight-color:transparent;

    &:hover {
      background: rgba(0, 0, 0, .025)
    }
  }

  .breadcrumb-container {
    float: left;
  }

  .right-menu {
    float: right;
    height: 100%;
    line-height: 50px;

    &:focus {
      outline: none;
    }

    .right-menu-item {
      display: inline-block;
      padding: 0 8px;
      height: 100%;
      font-size: 18px;
      color: #5a5e66;
      vertical-align: text-bottom;

      &.hover-effect {
        cursor: pointer;
        transition: background .3s;

        &:hover {
          background: rgba(0, 0, 0, .025)
        }
      }
    }

    .avatar-container {
      margin-right: 30px;

      .avatar-wrapper {
        margin-top: 5px;
        position: relative;

        .user-avatar {
          cursor: pointer;
          width: 40px;
          height: 40px;
          border-radius: 10px;
        }

        .el-icon-caret-bottom {
          cursor: pointer;
          position: absolute;
          right: -20px;
          top: 25px;
          font-size: 12px;
        }
      }
    }
  }
}
.first-menu-pannel{
    position: absolute;
    top: 45px;
    left: 10px;   
    width: 240px;
    z-index: 10;
    .el-icon-caret-top:before{
         font-size: 16px
    }
    .first-menu-table{
      padding: 10px 10px;
       background-color: rgba(0, 0, 0, .7);
       border-radius: 5px;
       border: 1px solid #efefef;
       color: white
    
    }
}
</style>
