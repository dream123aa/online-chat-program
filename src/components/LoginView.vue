<template>
  <el-container class="login-container">
    <el-main class="login-main">
      <div class="login-header animate__animated animate__fadeInDown">您好，欢迎来到在线聊天平台！</div>
      <el-form @submit.prevent="login" class="login-form animate__animated animate__zoomIn">
        <el-form-item>
          <el-input v-model="username" placeholder="用户名" prefix-icon="el-icon-user" class="animate-pulse"></el-input>
        </el-form-item>
        <el-form-item>
          <el-input v-model="password" type="password" placeholder="密码" prefix-icon="el-icon-lock" class="animate-pulse"></el-input>
        </el-form-item>
        <div class="form-links">
          <button @click="goToRegister" class="link-button">没有账号? 注册</button>
          <button @click="goToForgotPassword" class="link-button">忘记密码？</button>
        </div>
        <el-form-item>
          <el-button type="primary" @click="login" round block class="login-button animate-pulse">登录</el-button>
        </el-form-item>
      </el-form>
    </el-main>
  </el-container>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import { useRouter } from 'vue-router';
import { ElMessage } from 'element-plus';
import { useChatStore } from '../store';

export default defineComponent({
  name: 'LoginView',
  setup() {
    const router = useRouter();
    const chatStore = useChatStore();
    const username = ref('');
    const password = ref('');

    const login = () => {
      if (username.value.trim() === '123' && password.value.trim() === '123') {
        chatStore.setUser(username.value);
        ElMessage.success('登录成功！');
        router.push({ path: '/home', query: { username: username.value } });
      } else {
        ElMessage.error('用户名或密码错误');
      }
    };

    const goToRegister = () => {
      router.push('/register');
    };

    const goToForgotPassword = () => {
      router.push('/forgot-password');
    };

    return { username, password, login, goToRegister, goToForgotPassword };
  }
});
</script>

<style scoped>
.login-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.login-main {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100%;
}

.login-header {
  font-size: 2.5em;
  color: white;
  margin-bottom: 20px;
  text-align: center;
}

.login-form {
  width: 400px;
  background: rgba(255, 255, 255, 0.2);
  padding: 30px;
  border-radius: 10px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
}

.el-input {
  margin-bottom: 20px;
  border-radius: 5px;
  overflow: hidden;
}

.el-button {
  border-radius: 5px;
  transition: all 0.3s ease;
}

.form-links {
  display: flex;
  justify-content: space-between;
  margin-bottom: 20px;
}

.link-button {
  font-size: 0.9em;
  color: white;
  padding: 0;
  text-decoration: underline;
  cursor: pointer;
  border: none;
  background: none;
}

.login-button {
  width: 100%;
}
</style>