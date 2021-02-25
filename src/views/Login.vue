<template>
  <section>
    <div class="container">
      <div class="user singInBx">
        <div class="imgBx"><img src="../../status/image/singin.png" /></div>
        <div class="formBx">
          <form>
            <h2>Sign In</h2>
            <input type="text" placeholder="Username" v-model="name" />
            <input type="password" placeholder="Password" v-model="password" />
            <input type="submit" value="Login" @click.prevent="login" />
            <p class="singup">
              Don't have an account ?
              <a href="#" @click="toggleForm">Sign Up.</a>
            </p>
          </form>
        </div>
      </div>
      <div class="user singupBx">
        <div class="formBx">
          <form>
            <h2>Create an Account</h2>
            <input type="text" placeholder="Username" v-model="name" />
            <input type="text" placeholder="nickName" v-model="nickName" />
            <input
              type="password"
              placeholder="Create Password"
              v-model="password"
            />
            <input
              type="password"
              placeholder="Confirm Password"
              v-model="password2"
            />
            <input type="submit" value="Sign Up" @click.prevent="create" />
            <p class="singup">
              Already have an account ?
              <a href="#" @click="toggleForm">Sign in.</a>
            </p>
          </form>
        </div>
        <div class="imgBx"><img src="../../status/image/singin2.png" /></div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      name: "",
      password: "",
      password2: "",
      nickName: "",
    };
  },
  methods: {
    toggleForm() {
      var container = document.querySelector(".container");
      container.classList.toggle("active");
      this.name = "";
      this.password = "";
      this.password2 = "";
      this.nickName = "";
    },
    login() {
      this.$http({
        method: "post",
        url: "admin/signIn",
        data: {
          name: this.name,
          password: this.password,
        },
      }).then((e) => {
        console.log(e);
        if (e.data.status == 1) {
          localStorage.setItem("token", e.data.token);
          window.sessionStorage.setItem("type", e.data.type);
          localStorage.setItem("user_name", e.data.user_name);
          localStorage.setItem("nickName", e.data.nickName);
          localStorage.setItem("avatar", e.data.avatar);
          this.$store.commit('changeIsSignIn',2)
          this.$router.push("/home");
        } else {
          this.$message.error("账号或密码错误！");
        }
      });
    },
    create() {
      let that = this;
      if (this.password !== this.password2) {
        that.$message({
          type: "warning",
          message: "请确认两次密码相同！",
        });
        return;
      }
      if (that.name.length > 20) {
        that.$message({
          type: "warning",
          message: "登录账号太长!",
        });
        return;
      }
      if (that.nickName.length > 12) {
        that.$message({
          type: "warning",
          message: "昵称太长!",
        });
        return;
      }
      if (
        that.name.length == 0 ||
        that.nickName.length == 0 ||
        that.password.length == 0
      ) {
        that.$message({
          type: "warning",
          message: "有未填写项!",
        });
        return;
      }
      that
        .$http({
          url: "admin/signUp",
          method: "post",
          data: {
            name: that.name,
            password: that.password,
            nickName: that.nickName,
          },
        })
        .then((response) => {
          that.$message({
            type: "success",
            message: response.data.msg,
          });
          this.$router.push("/login");
          if (response.data.status == 1) {
            that.back();
          }
        })
        .catch((reject) => {
          console.log(reject);
        });
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Poppins", sans-serif;
}
section {
  position: relative;
  min-height: 100vh;
  background: #fee648;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px;
}
section .container {
  position: relative;
  width: 800px;
  height: 500px;
  background: #fff;
  box-shadow: 0 15px 50px rgba(0, 0, 0, 0.1);
  overflow: hidden;
}
section .container .user {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
}
section .container .user .imgBx {
  position: relative;
  width: 50%;
  height: 100%;
  background: #ff0;
  transition: 0.5s;
}
section .container .user .imgBx img {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
}
section .container .user .formBx {
  position: relative;
  width: 50%;
  height: 100%;
  background: #fff;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 40px;
  transition: 0.5s;
}
section .container .user .formBx form h2 {
  font-size: 18px;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 2px;
  text-align: center;
  width: 100%;
  margin-bottom: 10px;
  color: #555;
}
section .container .user .formBx form input {
  position: relative;
  width: 100%;
  padding: 10px;
  background: #f5f5f5;
  color: #333;
  border: none;
  outline: none;
  box-shadow: none;
  margin: 8px 0;
  font-size: 14px;
  letter-spacing: 1px;
  font-weight: 300;
}
section .container .user .formBx form input[type="submit"] {
  max-width: 100px;
  background: #677eff;
  color: #fff;
  cursor: pointer;
  font-size: 14px;
  font-weight: 500;
  letter-spacing: 1px;
  transition: 0.5s;
}
section .container .user .formBx form .signup {
  position: relative;
  margin-top: 20px;
  font-size: 12px;
  letter-spacing: 1px;
  color: #555;
  text-transform: uppercase;
  font-weight: 300;
}
section .container .user .formBx form .signup a {
  font-weight: 600;
  text-decoration: none;
  color: #677eff;
}
section .container .singupBx {
  pointer-events: none;
}
section .container.active .singupBx {
  pointer-events: initial;
}

section .container .singupBx .formBx {
  left: 100%;
}
section .container.active .singupBx .formBx {
  left: 0;
}
section .container .singupBx .imgBx {
  left: -100%;
}
section .container.active .singupBx .imgBx {
  left: 0;
}

section .container .singInBx .formBx {
  left: 0;
}
section .container.active .singInBx .formBx {
  left: 100%;
}
section .container .singInBx .imgBx {
  left: 0;
}
section .container.active .singInBx .imgBx {
  left: -100%;
}
@media (max-width: 991px) {
  section .container {
    max-width: 400px;
  }
  section .container .imgBx {
    display: none;
  }
  section .container .user .formBx {
    width: 100%;
  }
}
</style>
