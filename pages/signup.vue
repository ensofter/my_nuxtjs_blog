<template>
  <div class="text-center">
    <form class="form-signin" @submit.prevent="userRegister">
      <h1 class="h3 mb-3 mt-3 font-weight-normal">Для регистрации укажите имя пользователя и пароль</h1>
      <label for="inputUsername" class="sr-only">Имя пользователя</label>
      <input id="inputUsername" class="form-control" placeholder="Имя пользователя" required="" v-model="register.username">
      <label for="inputPassword" class="sr-only">Пароль</label>
      <input type="password" id="inputPassword" class="form-control mt-2" placeholder="Пароль" required="" v-model="register.password">
      <label for="ReInputPassword" class="sr-only">Повторите пароль</label>
      <input type="password" id="ReInputPassword" class="form-control mt-2" placeholder="Повторите пароль" required="" v-model="register.password2">
      <button class="btn mt-2 btn-lg btn-primary btn-block" type="submit">Регистрация</button>
    </form>
  </div>
</template>

<script>
export default {
  layout: "post_detail",
  data() {
    return {
      register: {
        username: '',
        password: '',
        password2: '',
      },
    }
  },
  methods: {
    async userRegister() {
      try {
        let response = await this.$axios.post('/api/register/', {
          username: this.register.username,
          password: this.register.password,
          password2: this.register.password2
        })
        console.log(response)
        await this.$auth.loginWith('local', {
          data: {
            username: this.register.username,
            password: this.register.password
          },
        })
        this.$router.push('/')
      } catch (err) {
        console.log(err)
      }
    }
  }
}
</script>

<style scoped>

</style>
