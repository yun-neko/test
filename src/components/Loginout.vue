<template>
  <div>
    <div>
      <table class="tab_css">
        <tr>
          <td rowspan="3" class="kuoda"></td>
          <td>
            <div class="ui samll input">
              <input
                type="text"
                v-model="loginForm.username"
                placeholder="用户名"
              />
            </div>
          </td>
        </tr>
        <tr>
          <td>
            <div class="ui samll input">
              <input
                type="text"
                v-model="loginForm.password"
                placeholder="密码"
              />
            </div>
          </td>
        </tr>
        <tr>
          <td>
            <span>&nbsp;</span>&nbsp;&nbsp;&nbsp;&nbsp;<span
              class="btn-order"
              @click="login"
              >登&nbsp;&nbsp;录</span
            >

            <span>&nbsp;</span>&nbsp;&nbsp;&nbsp;&nbsp;<span
              class="btn-pay"
              @click="login2"
              >注&nbsp;&nbsp;册</span
            >
          </td>
        </tr>
      </table>
    </div>

    <div class="banner-pay">
      <span>&nbsp;</span>&nbsp;&nbsp;&nbsp;&nbsp;<span
        class="btn-home"
        @click="rehome"
        >返&nbsp;&nbsp;回&nbsp;&nbsp;首&nbsp;&nbsp;页</span
      >
    </div>
  </div>
</template>
 
<script>
import { mapMutations } from "vuex";
export default {
  data() {
    return {
      loginForm: {
        username: "",
        password: "",
      },
    };
  },

  methods: {
    ...mapMutations(["changeLogin"]),
    login() {
      let _this = this;
      if (this.loginForm.username === "" || this.loginForm.password === "") {
        alert("账号或密码不能为空");
      } else {
        this.axios({
          method: "post",
          url: "/user/login",
          data: _this.loginForm,
        })
          .then((res) => {
            console.log(res.data);
            _this.userToken = "Bearer " + res.data.data.body.token;
            // 将用户token保存到vuex中
            _this.changeLogin({ Authorization: _this.userToken });
            _this.$router.push("/home");
            alert("登陆成功");
          })
          .catch((error) => {
            alert("账号或密码错误");
            console.log(error);
          });
      }
    },

    rehome() {
      this.$router.push({
        path: "/",
      });
    },
    log2() {
      this.$router.push({
        path: "#",
      });
    },
  },
};
</script>

<style scoped>
.tab_css {
  background-image: url("../../static/images/loginout.jpg");
  margin: 0 auto;
  width: 989px;
}
td {
  height: 40px;
}

.kuoda {
  width: 600px;
  height: 350px;
}
.banner-pay {
  border-top: 1px solid #ebeef5;
  padding: 15px 5px;
  overflow: hidden;
  text-align: right;
  color: #777;
}
.btn-home {
  display: inline-block;
  width: 120px;
  cursor: pointer;
  line-height: 36px;
  text-align: center;
  color: #fff;
  background-color: #42a5f5;
  user-select: none;
  transition: background-color 0.2s linear;
}
.btn-order {
  display: inline-block;
  width: 120px;
  cursor: pointer;
  line-height: 36px;
  text-align: center;
  color: #fff;
  background-color: #ffca28;
  user-select: none;
  transition: background-color 0.2s linear;
}
.btn-pay {
  display: inline-block;
  width: 120px;
  cursor: pointer;
  line-height: 36px;
  text-align: center;
  color: #fff;
  background-color: #95bf47;
  user-select: none;
  transition: background-color 0.2s linear;
}


</style>