<template>
  <div>
    <div class="text-center">
      <form class="form-signin" @submit.prevent="userLogin">
        <h1 class="h3 mb-3 mt-3 font-weight-normal">Пожалуйста укажите логин и пароль {{username}}</h1>
        <label for="inputUsername" class="sr-only">Имя пользователя</label>
        <input id="inputUsername" class="form-control" placeholder="Имя пользователя" required="" v-model="login.username">
        <label for="inputPassword" class="sr-only">Пароль</label>
        <input type="password" id="inputPassword" class="form-control mt-2" placeholder="Пароль" required="" v-model="login.password">
        <button class="btn mt-2 btn-lg btn-primary btn-block" type="submit">Войти</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  layout: "post_detail",
  data() {
    return {
      login: {
        username: '',
        password: ''
      },
      username: this.$auth.user
    }
  },
  methods: {
    async userLogin() {
      try {
        await this.$auth.loginWith('local', { data: this.login })
          .then((resp) => {
            this.$auth.setToken('local', 'Bearer ' + resp.data.access)
            this.$auth.setRefreshToken('local', resp.data.refresh)
            this.$axios.setHeader('Authorization', 'Bearer ' + resp.data.access)
            this.$auth.ctx.app.$axios.setHeader('Authorization', 'Bearer ' + resp.data.access)
            this.$axios.get('/api/profile').then((resp) => { this.$auth.setUser(resp.data.user.username); this.$router.push('/') })
          })
      } catch (err) {
      }
    }
  }
}
</script>

<style scoped>

</style>
