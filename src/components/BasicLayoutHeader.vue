<template>
  <header class="page-header">
    <div class="header-content container-1080">
      <div class="header-hd">
        <router-link :to="{ name: 'Home' }">
          <img
            class="header-logo"
            src="~@/assets/img/common/jiker-logo-black.svg"
          />
        </router-link>
        <nav class="header-nav">
          <router-link :to="{ name: 'Home' }" class="header-nav-item"
            >首页</router-link
          >
          <router-link :to="{ name: 'Zhiye' }" class="header-nav-item"
            >职业课</router-link
          >
          <router-link :to="{ name: 'Project' }" class="header-nav-item"
            >企业项目</router-link
          >
          <router-link :to="{ name: 'Evaluation' }" class="header-nav-item"
            >技能测评</router-link
          >
        </nav>
      </div>
      <div class="header-ft">
        <div
          class="bar-info-container"
          v-if="!userInfo.id"
          @click="handleNavToLogin"
        >
          <span class="header-loginandregister">登录</span>
          <el-divider direction="vertical"></el-divider>
          <span class="header-loginandregister">注册</span>
        </div>
        <el-dropdown
          style="height: 100%;"
          @command="handleCommand"
          v-if="userInfo.id"
        >
          <div class="bar-info-container">
            <i
              v-if="!userInfo.avatar_url"
              class="el-icon-user-solid userInfo-avatar"
            ></i>
            <img v-else class="userInfo-avatar" :src="userInfo.avatar_url" />
            <span class="userInfo-name">{{ userInfo.realname }}</span>
            <i class="el-icon-arrow-down el-icon--right"></i>
          </div>
          <el-dropdown-menu slot="dropdown">
            <el-dropdown-item icon="el-icon-user" command="GoMy"
              >个人设置</el-dropdown-item
            >
            <el-dropdown-item icon="el-icon-setting" command="GoSetting"
              >账号安全</el-dropdown-item
            >
            <el-dropdown-item icon="el-icon-document" command="GoResume"
              >个人简历</el-dropdown-item
            >
            <el-dropdown-item
              icon="el-icon-video-pause"
              command="Logout"
              divided
              >退出</el-dropdown-item
            >
          </el-dropdown-menu>
        </el-dropdown>
      </div>
    </div>
  </header>
</template>
<script type="text/javascript">
import { mapState } from "vuex";
import DataStore from "@/globals/storage/index";
export default {
  data() {
    return {};
  },
  computed: {
    ...mapState(["userInfo"])
  },
  methods: {
    handleCommand(command) {
      this[`handle${command}`]();
    },
    handleGoMy() {
      this.$router.push({ name: "My" });
    },
    handleGoSetting() {
      this.$router.push({ name: "Setting" });
    },
    handleGoResume() {
      this.$router.push({ name: "ResumeSetting" });
    },
    handleNavToLogin() {
      this.$router.push({ name: "AuthPhoneLogin" });
    },
    handleLogout() {
      DataStore.removeToken();
      window.location.reload();
    }
  }
};
</script>

<style type="text/css" lang="less" scoped>
.page-header {
  background-color: #fff;
  box-shadow: 0px 0px 10px 0px rgba(0, 0, 0, 0.05);
  .header-content {
    display: flex;
    justify-content: space-between;
    align-items: center;
    height: 60px;

    .header-hd,
    .header-bd,
    .header-ft {
      display: flex;
      align-items: center;
      height: 100%;
    }

    .header-logo {
      height: 40px;
      min-width: 40px;
      margin-right: 40px;
      vertical-align: middle;
    }

    .header-nav {
      display: inline-block;
      .header-nav-item {
        position: relative;
        font-size: 14px;
        line-height: 40px;
        color: #666;
        margin-right: 32px;
        text-decoration: none;
        &.router-link-exact-active {
          color: #333;
          &:after {
            position: absolute;
            content: "";
            width: 110%;
            height: 4px;
            background: #333;
            bottom: -8px;
            left: 50%;
            transform: translateX(-50%);
            border-radius: 2px;
          }
        }
      }
    }

    .page-header-right {
      height: 100%;
    }

    .bar-info-container {
      display: flex;
      align-items: center;
      height: 100%;
      padding: 0 10px;
      transition: all 0.2s ease;
      cursor: pointer;
      &:hover {
        background-color: #ecf5ff;
      }
      .userInfo-name {
        font-size: 14px;
        vertical-align: middle;
      }
      .userInfo-avatar {
        display: inline-block;
        width: 20px;
        height: 20px;
        line-height: 20px;
        text-align: center;
        background-color: #ccc;
        border-radius: 50%;
        outline: none;
        margin: 0 10px;
      }
    }
  }
  .header-loginandregister {
    color: #666;
  }
}
</style>
