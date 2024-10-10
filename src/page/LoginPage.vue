<script setup>
import { ref } from "vue";
import { useRouter } from "vue-router";
import axios from "axios";
const router = useRouter();
const giteedata = ref({
  grant_type: "password",
  username: "1539968872@qq.com",
  password: "153weishousong",
  client_id: "47c6365db10a1c95f7c810bf39604b00d06f7b1b67d8f4a782f84a49c36a1dde",
  client_secret:
    "c4e353626d74bef82d898bfb0f6d867994d1007dbac2f13c37963676e68cc29f",
  scope: "projects",
});
const handleClick = () => {
  axios
    .post("https://gitee.com/oauth/token", giteedata.value)
    .then((res) => {
      if (res.data.access_token != "") {
        router.push("/CodePage");
      } else {
        alert("登录出现错误");
      }
      console.log(res.data);
    })
    .catch((err) => {
      console.log(err);
    });
};
</script>
<template>
  <header>
    <section>
      <img src="../static/images/appm3V1L6Y3C3podIGShCo686dXRRY4i.png" />
    </section>
    <div class="biglogin">
      <div class="loginbox">
        <h1 style="text-align: center">登录，即刻创造您的应用</h1>
        <div class="switchlogin">
          <p>手机号登陆</p>
          <p>账号密码登录</p>
        </div>
        <div class="textinput">
          <p>
            <el-input
              v-model="giteedata.username"
              style="width: 350px; height: 50px"
              placeholder="账号"
            />
          </p>
          <p>
            <el-input
              v-model="giteedata.password"
              style="width: 350px; height: 50px"
              type="password"
              placeholder="密码"
              show-password
            />
          </p>
        </div>
        <div style="display: flex; align-items: center">
          <p><el-checkbox label="" size="large" /></p>
          <p>
            我已阅读并同意<span style="color: #032bec; margin: 0 5px 0 5px"
              >服务协议</span
            >和<span style="color: #032bec; margin: 0 5px 0 5px">隐私协议</span>
          </p>
        </div>
        <el-button @click="handleClick" color="#032bec">登录</el-button>
        <p style="text-align: center">
          <span>还未注册？</span>
          <span style="color: #032bec">立即注册</span>
        </p>
      </div>
    </div>
  </header>
</template>
<style scoped>
header,
.switchlogin,
.biglogin,
.loginbox,
.textinput {
  display: flex;
}

img {
  width: 40vw;
  height: 99.5vh;
}

.biglogin {
  width: 50vw;
  height: 100vh;
  justify-content: center;
  align-items: center;
}

.loginbox {
  justify-content: center;
  flex-direction: column;
}

.switchlogin {
  justify-content: space-around;
}

.textinput {
  align-items: center;
  flex-direction: column;
}
</style>
