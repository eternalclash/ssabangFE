<template>
  <div class="signup-container">
    <div class="input-container">
      <div class="logo-group">
        <div class="logo"></div>
      </div>
      <div class="input-group">
        <input type="text" v-model="name" placeholder="이름" required />
      </div>
      <div class="input-group">
        <input type="email" v-model="email" placeholder="아이디 (이메일)" required />
      </div>
      <div class="input-group">
        <input type="password" v-model="password" placeholder="비밀번호" required />
      </div>
      <div class="input-group">
        <input type="password" v-model="confirmPassword" placeholder="비밀번호 재확인" required />
      </div>

      <button class="signup-button" @click="signup">회원가입</button>
      <button class="login-button" @click="goToLogin">로그인 페이지로 돌아가기</button>
    </div>
  </div>
</template>

<script>
import { postSignup } from '@/api/loginAPI'

export default {
  name: 'SignUpContainer',
  data() {
    return {
      email: '',
      name: '',
      password: '',
      confirmPassword: ''
    }
  },
  methods: {
    async signup() {
      if (this.password !== this.confirmPassword) {
        alert('비밀번호가 일치하지 않습니다.')
        return
      }
      if (
          this.name == null ||
          this.name == '' ||
          this.email == null ||
          this.email == '' ||
          this.password == null ||
          this.password == ''
        ) {
          alert('아이디,이름,비밀번호에 공백이 존재합니다.')
          return
        }
      try {
        const userData = {
          email: this.email,
          name: this.name,
          password: this.password
        }
        const result = await postSignup(userData)
        alert('회원가입 성공!')
        this.$router.push({ name: 'LoginContainer' })
      } catch (error) {
        alert('존재하는 아이디입니다.')
      }
    },
    goToLogin() {
      this.$router.push({ name: 'LoginContainer' })
    }
  }
}
</script>

<style scoped>
.signup-button {
  margin-top: 2vh;
  width: 100%;
  border-radius: 5px;
  border: none;
  color: white;
  background-color: #2462b9;
  box-shadow: 4px 4px 8px #aaa;
  cursor: pointer;
  transition: background-color 0.3s;
  padding: 3%;
}
.login-button {
  width: 100%;
  border-radius: 5px;
  border: none;
  color: white;
  background-color: #484854;
  box-shadow: 4px 4px 8px #aaa;
  cursor: pointer;
  transition: background-color 0.3s;
  padding: 3%;
  margin-top: 2vh;
}
.logo-group {
  display: flex;
  width: 100%;
  height: 20vh;
  justify-content: center;
}
.logo {
  width: 100%;
  height: auto;
  background-repeat: no-repeat;
  background-color: transparent;
  background-image: url('@/assets/SSABANG.svg');
  background-size: contain;
  background-position: center;
}
.signup-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 90vh;
  position: relative;
  overflow: hidden;
}
.signup-container::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #cae5ff;
  opacity: 0.5;
}
.input-container {
  position: relative;
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
  width: 30%;
  padding: 3%;
  border-radius: 1%;
}
.input-group {
  margin-bottom: 3vh;
  width: 100%;
}
input[type='text'],
input[type='email'],
input[type='password'] {
  border: none;
  height: 5vh;
  width: 98%;
  border-radius: 5px;
  outline: none;
  font-size: 16px;
  padding-left: 2%;
}
button:hover {
  opacity: 0.5;
  background-color: rgba(0, 0, 0, 0.3);
}
</style>
