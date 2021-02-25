<template>
  <div id="container">
    <div class="header" id="header">
      <!-- 导航栏1开始 -->

      <div class="nav" id="nav1">
        <div class="nav-inner">
          <el-menu
            class="el-menu-demo"
            mode="horizontal"
            :background-color="bgcstatus ? '#2d2e30' : 'rgba(242, 244, 248, 0)'"
            text-color="#f5f6f7"
            active-text-color="#ffd04b"
            :router="true"
          >
            <el-menu-item index="/home"
              ><i class="el-icon-s-home"></i>首页</el-menu-item
            >
            <el-menu-item index="/modules"
              ><i class="el-icon-menu"></i>组件</el-menu-item
            >
            <el-menu-item index="/clockin"
              ><i class="el-icon-s-claim"></i>打卡</el-menu-item
            >
            <el-menu-item index="/aboutme"
              ><i class="el-icon-s-custom"></i>关于作者</el-menu-item
            >
            <!-- <a
              href="#"
              class="loginNav"
              @click.prevent="$router.push({ name: 'Login' })"
              >登入</a
            > -->
            <el-dropdown trigger="click" style="float:right;margin:5px">
              <el-avatar :src="this.type ? avatar : ''"></el-avatar>
              <!-- <img :src="avatar"> -->
              <el-dropdown-menu slot="dropdown">
                <el-dropdown-item @click.native="login">{{
                  loginstatus
                }}</el-dropdown-item>

                <el-dropdown-item
                  v-show="type == 1"
                  @click.native="$router.push('/edit')"
                  >发布文章</el-dropdown-item
                >
                <el-dropdown-item @click.native="dialogFormVisible = true"
                  >修改信息</el-dropdown-item
                >
              </el-dropdown-menu>
            </el-dropdown>
          </el-menu>
        </div>
      </div>

      <!-- 导航栏1结束 -->
      <!-- 导航栏2 -->
      <div class="nav-min">
        <div class="nav-menu">
          <el-dropdown trigger="click">
            <span class="el-dropdown-link">
              <img
                src="../../status/image/menu.png"
                class="el-icon-arrow-down el-icon--right"
              />
            </span>

            <el-dropdown-menu slot="dropdown">
              <el-dropdown-item>首页</el-dropdown-item>
              <el-dropdown-item>主键</el-dropdown-item>
              <el-dropdown-item>关于作者</el-dropdown-item>
            </el-dropdown-menu>
          </el-dropdown>
        </div>
        <el-dropdown trigger="click" style="float:right;margin:5px">
          <el-avatar :src="avatar"></el-avatar>
          <!-- <img :src="avatar"> -->
          <el-dropdown-menu slot="dropdown">
            <el-dropdown-item @click.native="login">{{
              loginstatus
            }}</el-dropdown-item>

            <el-dropdown-item
              v-show="type == 1"
              @click.native="$router.push('/edit')"
              >发布文章</el-dropdown-item
            >
            <el-dropdown-item @click.native="dialogFormVisible = true"
              >修改信息</el-dropdown-item
            >
          </el-dropdown-menu>
        </el-dropdown>
      </div>
      <!-- 导航栏2结束 -->
      <div class="banner">
        <div class="header-banner-info">
          <div class="header-banner-info__title">zhang's Blog</div>
          <div class="header-banner-info__subtitle">
            Live a good life meet slowly
          </div>
        </div>
        <div class="header-banner-arrow" @click="goTo">
          <div class="header-banner-arrow__icon">
            <i class="el-icon-arrow-down"></i>
          </div>
        </div>
      </div>
    </div>

    <div class="main">
      <div class="main-inner">
        <div class="sidebar-wrap" id="sidebar-wrap" v-if="windowWidth > 992">
          <!-- 侧边栏1开始 -->
          <div class="sidebar">
            <el-card shadow="always" body-style="height:333px;padding:20px">
              <div>
                <img src="../../status/image/touxiang.jpg" />
                <h3>好好生活，慢慢相遇</h3>
                <div class="sidebar-icon">
                  <el-tooltip
                    class="item"
                    effect="dark"
                    content="GitHub"
                    placement="top-start"
                  >
                    <a href="https://github.com/zhang-wan-zhi" target="_blank">
                      <img src="../../status/image/github.png"
                    /></a>
                  </el-tooltip>
                  <el-tooltip
                    class="item"
                    effect="dark"
                    content="微博"
                    placement="top-start"
                  >
                    <a
                      href="https://weibo.com/3277546854/profile?topnav=1&wvr=6&is_all=1"
                      target="_blank"
                      ><img src="../../status/image/weibo.png"
                    /></a> </el-tooltip
                  ><el-tooltip
                    class="item"
                    effect="dark"
                    content="QQ"
                    placement="top-start"
                  >
                    <a href="http://wpa.qq.com/msgrd?v=3&uin=1392338713&site=qq&menu=yes" target="_blank"
                      ><img src="../../status/image/qq.png"
                    /></a> </el-tooltip
                  ><el-tooltip
                    class="item"
                    effect="dark"
                    content="简书"
                    placement="top-start"
                  >
                    <a href="https://www.jianshu.com/u/47adb37e1226" target="_blank"
                      ><img src="../../status/image/redbook.png"
                    /></a>
                  </el-tooltip>
                </div>
              </div>
              <div class="sidebar-save">
                <div class="sidebar-save-this" @click="AddFavorite">
                  <i class="el-icon-location"></i><span>收藏本页</span>
                </div>
                <div class="sidebar-save-emil">
                  <i class="el-icon-message"></i><span>邮箱订阅</span>
                </div>
              </div>
            </el-card>
          </div>
          <!-- 侧边栏1结束 -->
          <!-- 侧边栏2开始 -->
          <div class="sidebar2">
            <el-card shadow="always" body-style="padding:20px">
              <div class="sidebar2-tag">
                <el-tag
                  @click="subtotal(item.list)"
                  v-for="item in items"
                  :key="item.type"
                  style="margin:0 10px 10px 0;cursor: pointer;"
                  >#{{ item.type }}</el-tag
                >
              </div>
            </el-card>
          </div>
          <!-- 侧边栏2结束 -->
          <!-- 侧边栏3开始 -->
          <div class="sidebar3">
            <el-card shadow="always" body-style="padding:20px 0 0px 20px">
              <div class="megs">
                <ul
                  class="infinite-list"
                  v-infinite-scroll="loadmsg"
                  style="overflow:auto"
                  infinite-scroll-immediate="false"
                >
                  <li
                    v-for="item in msglists"
                    class="infinite-list-item"
                    :key="item._id"
                    style="display:flex;height:90px"
                  >
                    <el-avatar
                      shape="square"
                      size="small"
                      :src="item.pic"
                    ></el-avatar>
                    <div class="msgmain">
                      <div class="nickName">{{ item.nickName }}</div>
                      <el-tooltip
                        :content="item.message"
                        placement="bottom"
                        effect="light"
                      >
                        <div class="message">{{ item.message }}</div>
                      </el-tooltip>
                      
                    </div>
                  </li>
                </ul>
              </div>
              <div class="sendMsg">
                <span>留下你的话吧...</span>
                <el-button
                  type="primary"
                  icon="el-icon-edit"
                  circle
                  @click="sendMsg"
                  style="margin:10px 20px 10px 0"
                ></el-button>
              </div>
            </el-card>
          </div>
          <!-- 侧边栏3结束 -->
        </div>
        <div class="content-wrap">
          <router-view></router-view>
        </div>
      </div>
    </div>
    <el-dialog title="修改信息" :visible.sync="dialogFormVisible">
      <el-form :model="form">
        <el-form-item label="修改昵称">
          <el-input v-model="nickName" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="头像">
          <label for="upLoad">
            <img :src="avatar" class="avatar" />
          </label>
          <input
            @change="upLoad"
            id="upLoad"
            type="file"
            style="display:none"
          />
          <p class="tips">tips:请上传2M以内JPG/PNG格式的图片，比例最好1:1</p>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogFormVisible = false">取 消</el-button>
        <el-button type="primary" @click="save">确 定</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
import { imgTo64 } from "../../status/js/public.js";
export default {
  data() {
    return {
      items: [],
      loginstatus: "",
      type: "",
      avatar: "",
      dialogFormVisible: false,
      form: {
        nickName: "",
        avatar: "",
      },
      name: "",
      token: "",
      windowWidth: document.body.clientWidth,
      bgcstatus: false,
      nickName: "",
      msglists: [],
      page: 0,
      nomsglist: false,
    };
  },
  methods: {
    loadmsg() {
      if (this.nomsglist) {
        console.log("111",this.nomsglist);
        return;
      }
      this.$http({
        method: "post",
        url: "messagelist",
        data: {
          page: this.page,
          rows: 4,
        },
      }).then((e) => {
        this.page = this.page + 1;
        if (e.data.status) {
          this.nomsglist = true;
        }
        for (let i = 0; i < e.data.length; i++) {
          let obj = {
            page: e.data[i].page,
            _id: e.data[i]._id,
            nickName: e.data[i].nickName,
            message: e.data[i].message,
            type: e.data[i].type,
            pic: e.data[i].pic,
          };
          this.msglists.push(obj);
        }
        console.log("第nc", e);
        console.log("lieb", this.msglists);
      });
    },
    goTo() {
      var hd = document.getElementById("header");
      var headerwid = hd.offsetHeight;
      window.scrollTo(0, headerwid);
    },
    save() {
      //保存
      let that = this;
      that
        .$http({
          method: "post",
          url: "admin/updateUser",
          data: {
            name: that.name,
            token: that.token,
            nickName: that.nickName,
            avatar: that.avatar,
          },
        })
        .then((response) => {
          alert(response.data.msg);
          this.dialogFormVisible = false;
          if (response.data.status == 1) {
            localStorage.setItem("nickName", response.data.nickName);
            localStorage.setItem("avatar", response.data.avatar);
          }
        })
        .catch((reject) => {
          console.log(reject);
        });
    },
    subtotal(e) {
      this.$store.commit("increment", e);
      console.log("e", e);
      console.log("path", this.$route.path);
      if (this.$route.path == "/home/subtotal") {
        this.$router.push("/home");
        setTimeout(() => {
          this.$router.push("/home/subtotal");
        }, 100);
      } else {
        this.$router.push("/home/subtotal");
      }
    },
    login() {
      if (this.loginstatus === "登入") {
        this.$router.push("/login");
      } else {
        /* localStorage.removeItem("token"); */
        sessionStorage.removeItem("type");
        this.$store.commit("changeIsSignIn", 0);
        localStorage.clear();
        this.loginstatus = "登入";
        this.type = 0;
      }
    },
    //收藏本站

    AddFavorite(title, url) {
      try {
        window.external.addFavorite(url, title);
      } catch (e) {
        try {
          window.sidebar.addPanel(title, url, "");
        } catch (e) {
          alert(
            "抱歉，您所使用的浏览器无法完成此操作。\n\n加入收藏失败，请使用Ctrl+D进行添加"
          );
        }
      }
    },
    upLoad(e) {
      //上传头像
      let that = this;
      let files = e.target.files || e.dataTransfer.files;

      if (!files.length) return;
      if (
        files[0].type.indexOf("png") > -1 ||
        files[0].type.indexOf("jpg") > -1 ||
        files[0].type.indexOf("jpeg") > -1
      ) {
        if (files[0].size < 2000000) {
          if (typeof FileReader === "undefined") {
            alert("您的浏览器不支持图片上传，请升级您的浏览器");
          }
          let reader = new FileReader();
          reader.readAsDataURL(files[0]);
          reader.onload = function(e) {
            let image = new Image();
            image.src = e.target.result; //原始base64
            image.setAttribute("crossOrigin", "anonymous"); //允许图片跨域请求、必须后台也允许
            image.onload = () => {
              let base64 = imgTo64(image); //使用cavas压缩
              that.avatar = base64;
            };
          };
        } else {
          alert("请上传2M以内的图片");
        }
      } else {
        alert("请上传JPG/PNG格式的图片");
      }
    },
    sendMsg() {
      
      this.$prompt("", "留言板", {
        confirmButtonText: "确定",
        cancelButtonText: "取消",
      })
        .then(({ value }) => {
          this.nomsglist = false
          this.$http({
            method: "post",
            url: "message/save",
            data: {
              messagesForm: {
                name: this.nickName,
                message: value,
                type: this.type + "",
                pic: this.avatar,
              },
            },
          });
          this.$message({
            type: "success",
            message: "留言成功啦...",
          });
        })
        .catch(() => {
          this.$message({
            type: "info",
            message: "取消输入",
          });
        });
    },
  },
  mounted() {
    // 判断是否登入
    this.type = sessionStorage.getItem("type");
    this.loginstatus = this.type ? "退出" : "登入";
    var hd = document.getElementById("header");
    var headerwid = hd.offsetHeight;
    var side = document.getElementById("sidebar-wrap");
    /* 导航栏 */
    var nav = document.getElementById("nav1"); //导航栏
    var scrollTop = 0,
      topValue = getScrollTop();
    document.onscroll = function() {
      /* 侧边栏固定 */
      if (side) {
        var wid = side.offsetWidth;
        
        //获取距离页面顶端的距离
        //滚动事件

        //获取当前滚动的距离
        var btop =
          document.body.scrollTop || document.documentElement.scrollTop;

        //如果滚动距离大于导航条据顶部的距离
        if (btop > headerwid) {
          
          //为导航条设置fix
          side.className = "sidebar-wrap-active";
          side.style.width = wid + "px";
        } else {
          side.className = "sidebar-wrap";
        }
      }
      /* 侧边栏固定 */
      if (document.body.clientWidth < 983) {
        return;
      }

      if (btop == 0) {
        nav.className = "nav";
        this.bgcstatus = false;
      } else {
        scrollTop = getScrollTop();
        if (scrollTop <= topValue) {
          // 上滑
          nav.className = "nav-active";
          this.bgcstatus = true;
          startmove(0);
        } else {
          // 下滑
          if (btop < 200) {
            nav.className = "nav-active";
            this.bgcstatus = true;
          } else if (btop > 200) {
            startmove(-60);
          } else {
            nav.className = "nav"; // 等同于消失
          }
        }
        setTimeout(function() {
          topValue = scrollTop;
        }, 0);
      }
    };
    function getScrollTop() {
      var scrollTop = 0;
      if (document.documentElement && document.documentElement.scrollTop) {
        scrollTop = document.documentElement.scrollTop;
      } else if (document.body) {
        scrollTop = document.body.scrollTop;
      }
      return scrollTop;
    }
    // 收缩效果
    var timer;
    function startmove(target) {
      clearInterval(timer); //清除定时器，以免多次触发定时器导致速度越来越快而不是匀速前进
      timer = setInterval(function() {
        var speed = 0;
        if (nav.offsetTop > target) {
          speed = -10;
        } else {
          speed = 10;
        }
        if (nav.offsetTop == target) {
          clearInterval(timer);
        } else {
          nav.style.top = nav.offsetTop + speed + "px";
        }
      }, 20);
    }
    /* 导航栏 */
    var that = this;
    // <!--把window.onresize事件挂在到mounted函数上-->
    window.onresize = () => {
      return (() => {
        window.fullWidth = document.documentElement.clientWidth;
        that.windowWidth = window.fullWidth; // 宽
      })();
    };
  },
  created() {
    this.avatar = localStorage.getItem("avatar");
    this.name = localStorage.getItem("user_name");
    this.nickName = localStorage.getItem("nickName");
    this.token = localStorage.getItem("token");
    this.$http({
      method: "post",
      url: "articleList",
      data: {
        type: "categories",
      },
    }).then((e) => {
      console.log('这个是e',e);
      this.items = e.data;
    });
    // 留言列表
    this.$http({
      method: "post",
      url: "messagelist",
      data: {
        page: 1,
        rows: 4,
      },
    }).then((e) => {
      console.log(e);
      this.msglists = e.data;
      this.page = e.data[0].page;
      this.page = this.page + 1;
    });
  },
  watch: {
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
#container {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 100%;
}

.main {
  width: 100%;
  height: 100%;
  margin-top: 10px;
}

.main-inner {
  width: 1200px;
  height: 100%;
  margin: 0 auto;
  position: relative;
}

.sidebar-wrap {
  width: 22%;
  float: left;
}

.sidebar-wrap-active {
  width: 22%;
  position: fixed;
  top: 0;
}
.sidebar3 .sendMsg {
  display: flex;
  justify-content: space-between;
}
.sidebar3 .sendMsg span {
  height: 60px;
  line-height: 60px;
}
.sidebar3 .megs ul {
  height: 300px;
}
.sidebar3 {
  height: 400px !important;
  overflow: hidden;
  margin-top: 20px;
}

.sidebar3 .msgmain .message {
  width: 170px;
  height: 30px;
  overflow: hidden;
  font-size: 6px;
  text-align: left;
  margin-left: 10px;
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 2;
}
.sidebar3 .msgmain .nickName {
  height: 28px;
  text-align: left;
  margin-left: 10px;
}
.content-wrap {
  width: 77%;
  margin: 0 auto;
  float: right;
}

.loginNav {
  float: right;
  height: 60px;
  line-height: 60px;
  text-decoration: none;
  outline: none;
}

.nav {
  display: flex;
  position: absolute;
  z-index: 1;
  width: 100%;
  height: 60px;
  background-color: rgba(242, 244, 248, 0);
}

.nav-active {
  position: fixed;
  display: flex;
  z-index: 9999;
  width: 100%;
  height: 60px;
  background-color: #2d2e30;
}

.nav .el-menu-item {
  font: 18px "PingFang SC" !important;
  line-height: 50px !important;
}

.nav .el-submenu__title {
  font: 18px "PingFang SC" !important;
  line-height: 50px !important;
  background-color: #2d2e30 !important;
}

.nav-inner {
  margin: 0 auto;
  padding: 20px;
  padding-top: 0 !important;
  padding-bottom: 0 !important;
  width: 1100px;
  height: 100%;
}

.nav-active .el-menu-item {
  font: 18px "PingFang SC" !important;
  line-height: 50px !important;
}

.nav-active .el-submenu__title {
  font: 18px "PingFang SC" !important;
  line-height: 50px !important;
  background-color: #2d2e30 !important;
}

.banner {
  position: relative;
  z-index: 0;
  width: 100%;
  height: 100%;
  background: url(../../status/image/nav1.png) no-repeat center/cover;
}

.banner .header-banner-info {
  position: absolute;
  top: 40%;
  left: 0;
  padding: 0 0.5rem;
  width: 100%;
  text-align: center;
}

.banner .header-banner-info .header-banner-info__title {
  margin-bottom: 2rem;
  font-size: 4rem;
  font-weight: 700;
  line-height: 1;
  color: #f5f6f7;
}

.banner .header-banner-info .header-banner-info__subtitle {
  font-size: 1.2rem;
  font-weight: 400;
  color: #f5f6f7;
}

.banner .header-banner-arrow {
  position: absolute;
  left: 50%;
  cursor: pointer;
  transform: translate(-50%, -50%);
  text-align: center;
  margin-left: -1%;
  animation-name: beat; /*动画名称*/
  animation-duration: 2s; /*设置秒数*/
  animation-timing-function: linear; /*速度曲线*/
  animation-iteration-count: infinite; /*播放次数*/
  animation-direction: alternate; /*逆向播放*/
  animation-play-state: running; /*正在运行*/
}

.banner .header-banner-arrow__icon {
  width: 100%;
  height: 100%;
  font-size: 2rem;
  font-weight: 700;
  line-height: 1;
  text-align: center;
  color: #fff;
}

@keyframes beat {
  0% {
    bottom: 5%;
  }

  50% {
    bottom: 2%;
  }

  100% {
    bottom: 5%;
  }
}

.header {
  width: 100%;
  font-size: 18px;
  background-color: #2d2e30;
  height: 80vh;
}

.main-inner {
  position: relative;
}

.sidebar {
  width: 100%;
  height: 337px;
}

.sidebar2 {
  width: 100%;
  margin-top: 20px;
}

.sidebar img {
  width: 120px;
  height: 120px;
  border-radius: 50%;
  border: none;
  outline: none;
}

.sidebar a {
  border: none;
  outline: none;
}

.sidebar .sidebar-save {
  display: flex;
  justify-content: space-around;

  font-size: 16px;
}

.sidebar .sidebar-save .sidebar-save-this {
  cursor: pointer;
  color: #058ed2;
}

.sidebar .sidebar-save .sidebar-save-emil {
  cursor: pointer;
  color: #ff5956;
}

.sidebar .sidebar-icon {
  display: flex;
  justify-content: space-around;
  margin-top: 25px;
}

.sidebar2 .sidebar2-tag {
  display: flex;
  flex-wrap: wrap;
}

.sidebar .sidebar-icon a {
  display: inline-block;
  width: 32px;
  height: 32px;
}
.sidebar .sidebar-icon img {
  width: 32px;
  height: 32px;
}

.el-menu.el-menu--horizontal {
  border-bottom: none !important;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}

.header .nav-min {
  display: none;
  z-index: 1;
  position: absolute;
  width: 100%;
  height: 50px;
}

.header .nav-min .nav-menu {
  height: 32px;
  width: 32px;
  margin: 10px;
  cursor: pointer;
}

.avatar {
  width: 100px;
  height: 100px;
  display: block;
  margin: 0 auto;
  background: #eee;
  border-radius: 50%;
  cursor: pointer;
}

@media screen and (max-width: 1200px) {
  .main-inner {
    width: 100%;
    margin: 0 auto;
  }
}

@media screen and (max-width: 992px) {
  .sidebar-wrap {
    position: absolute;
    z-index: -100 !important;
  }
  .content-wrap {
    margin-top: 10px;
    width: 100%;
  }
  .header {
    height: 30vh;
  }
  .nav {
    display: none;
  }
  .header .nav-min {
    display: flex;
    justify-content: space-between;
  }
}
</style>
