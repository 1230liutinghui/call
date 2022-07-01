<template>
  <div class="header-nav">
    <div class="header-nav-left">
      <div class="header-nav-title">🦉猫头鹰助理模拟电话</div>
    </div>
    <div class="header-nav-help">
      <el-dropdown @command="handleCommand">
        <span class="el-dropdown-link">
          选项
          <i class="el-icon-arrow-down el-icon--right"></i>
        </span>
        <el-dropdown-menu slot="dropdown">
          <el-dropdown-item command="command-logout">退出</el-dropdown-item>
        </el-dropdown-menu>
      </el-dropdown>
    </div>
  </div>
</template>

<script>
import { setUserLoginInfo } from "../../utils";
export default {
  name: "HeaderNav",
  methods: {
    handleCommand: function(command) {
      if (command === "command-detect") {
        window.open(
          "https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html",
          "__blank"
        );
        return;
      }

      if (command === "command-logout") {
        this.$trtcCalling.logout();
        this.$store.commit("userLogoutSuccess");
        setUserLoginInfo({
          token: "",
          phoneNum: ""
        });
      }
    },
    gotoHomePage: function() {
      if (this.$router.currentRoute.fullPath !== "/") {
        this.$router.push("/");
      }
    }
  }
};
</script>

<style scoped>
.header-nav {
  font-size: 18px;
  background: #000623;
  height: 3em;
  display: flex;
  padding: 0 20%;
  justify-content: space-around;
  color: #ffffff;
  border: 1px #000000;
}
.header-nav-left {
  display: flex;
  flex-direction: row;
}
.header-nav-title {
  font-size: 18px;
  display: flex;
  align-items: center;
}
.header-nav-homepage {
  margin-left: 50px;
  font-size: 18px;
  display: flex;
  align-items: center;
  cursor: pointer;
}
.header-nav-help {
  font-size: 18px;
  display: flex;
  align-items: center;
}
.el-dropdown-link {
  color: #ffffff;
  font-size: 16px;
  cursor: pointer;
}
@media screen and (max-width: 767px) {
  .header-nav {
    padding: 0;
  }
  .header-nav-left {
    justify-content: space-around;
    width: 75%;
  }
  .header-nav-title,
  .el-dropdown-link {
    font-size: 18px;
  }
  .header-nav-homepage {
    font-size: 18px;
    margin-left: 10px;
  }
}
</style>
