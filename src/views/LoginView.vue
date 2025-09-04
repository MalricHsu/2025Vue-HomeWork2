<template>
  <div id="loginPage" class="bg-yellow">
    <div class="conatiner loginPage vhContainer">
      <div class="side">
        <a href="#"
          ><img
            class="logoImg"
            src="https://raw.githubusercontent.com/hexschool/2022-web-layout-training/main/todolist/logo.png"
            alt=""
        /></a>
        <img
          class="d-m-n"
          src="https://raw.githubusercontent.com/hexschool/2022-web-layout-training/main/todolist/img.png"
          alt="workImg"
        />
      </div>
      <div>
        <form class="formControls" action="index.html">
          <h2 class="formControls_txt">最實用的線上代辦事項服務</h2>
          <label class="formControls_label" for="email">Email</label>
          <input
            class="formControls_input"
            type="text"
            id="email"
            name="email"
            placeholder="請輸入 email"
            required
            v-model="email"
          />
          <span v-if="email === ''">此欄位不可留空</span>
          <label class="formControls_label" for="pwd">密碼</label>
          <input
            class="formControls_input"
            type="password"
            name="pwd"
            id="pwd"
            placeholder="請輸入密碼"
            required
            v-model="password"
          />
          <input class="formControls_btnSubmit" type="button" @click="handleLogin" value="登入" />
          <RouterLink class="formControls_btnLink" to="/register">註冊帳號</RouterLink>
        </form>
      </div>
    </div>
  </div>
</template>
<script setup>
import { ref } from 'vue'
import { RouterLink, useRouter } from 'vue-router'
import { login } from '@/utils/api'
const router = useRouter()

// 表單資料
const email = ref('')
const password = ref('')

const handleLogin = async () => {
  try {
    const response = await login(email.value, password.value)
    const { token, exp } = response.data
    // 儲存 token
    document.cookie = `vue3-todolist-token=${token}; expires=${exp}`
    router.push('/todolist')
    swal('登入成功！', '進入TodoList', 'success')
  } catch (error) {
    swal('登入失敗！', error.response.data.message, 'error')
  }
}
</script>
