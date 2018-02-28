<template>
  <header class="tx-header">
    <el-row type="flex" class="row-bg" justify="space-between">
      <el-col :lg="8" :md="8" class="logo">
        <span class="img-box" @click="$router.push('/')"><img src="../assets/img/logo.png"></span>
        <p class="title tx-md-hide">TailorX 工厂端</p>
        <span class="menu-icon tx-md-show" @click="clickMenu">
            <i class="iconfont icon-portal-icon-caidan"></i>
          </span>
      </el-col>
      <el-col :lg="8" :md="8" class="mobile-title">
        <span class="tx-md-show">TailorX</span>
      </el-col>
      <el-col :lg="8" :md="8" class="right-box">
        <div class="logout-box">
          <span style="color: #ffffff;margin-right: 20px" class="tx-md-hide" v-text="username"></span>
          <div class="logout-btn" @click="logout">
            <span class="ico-box"><i class="iconfont icon-tuichu"></i></span>
            <span class="text tx-md-hide">退出</span>
          </div>
        </div>
      </el-col>
    </el-row>
  </header>
</template>

<script>
  import Vue from 'vue'
  import store from 'store'
  import {row, input, col, MessageBox} from 'element-ui'

  Vue.use(row);
  Vue.use(col);
  Vue.use(input);

  export default {
    name: 'header',
    data: function () {
      return {
        username: ''
      }
    },
    created: function () {
      this.updateHeader({username: store.get('user') ? store.get('user').name : ''});
      this.$parent.$on('update-header', this.updateHeader);
    },
    methods: {
      clickMenu: function () {
        this.$parent.$emit('hide-menu');
      },
      updateHeader: function (params) {
        this.username = params.username;
      },
      logout: function () {
        let _this = this;
        MessageBox.confirm('是否确认退出登录？', '温馨提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          type: 'warning',
          callback: function (action) {
            if (action === 'confirm') {
              _this.$router.push('/login');
            }
          }
        })
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .tx-header {
    position: fixed;
    height: 70px;
    top: 0;
    left: 0;
    width: 100%;
    z-index: 2;
    background-color: #3f3f3f;
    transition: all .5s;
  }

  .tx-header.fullScreen {
    display: none;
  }

  .tx-header .logo {
    line-height: 70px;
    text-align: left;
  }

  .tx-header .img-box {
    display: inline-block;
    text-align: center;
    position: relative;
    margin: 0 10px 0 30px;
    cursor: pointer;
  }

  .tx-header .logo img {
    width: 50px;
    vertical-align: middle;
    display: inline-block;
  }

  .tx-header .mobile-title,
  .tx-header .title {
    color: #ffffff;
    display: inline-block;
    vertical-align: middle;
    font-size: 24px;
    line-height: 0;
    margin-left: 20px;
  }

  .tx-header .logout-box {
    padding-right: 30px;
    padding-left: 30px;
  }

  .tx-header .logout-btn {
    display: inline-block;
    cursor: pointer;
  }

  .tx-header .logout-btn:hover span {
    color: #eaeaea;
  }

  .tx-header .right-box {
    line-height: 70px;
    text-align: right;
  }

  .tx-header .ico-box {
    width: 38px;
    height: 38px;
    display: inline-block;
    line-height: 38px;
    border-radius: 50%;
    text-align: center;
    vertical-align: middle;
    background-color: #2f2f2f;
    color: #9f9f9f;
    font-size: 18px;
  }

  .tx-header .right-box .text {
    color: #d8d8d8;
    font-size: 14px;
    margin-left: 10px;
  }

  .tx-header .menu-icon {
    width: 35%;
    display: inline-block;
    vertical-align: top;
    margin-left: 20px;
    margin-top: 3px;
  }

  .tx-header .menu-icon i {
    font-size: 34px;
    color: #ffffff;
  }

  .tx-header .mobile-title {
    text-align: center;
    line-height: 70px;
    margin-left: 0;
  }

</style>
