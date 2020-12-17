<template>
  <div>
    <Header :h1="title"/>
  <div class="container">
    <div class="row">
      <div class="col-lg-12">
        <nav aria-label="breadcrumb" class="mt-4">
          <ol class="breadcrumb">
            <li class="breadcrumb-item"><nuxt-link to="/">Главная</nuxt-link></li>
            <li class="breadcrumb-item active" aria-current="page">Контакты</li>
          </ol>
        </nav>
        <p class="lead">Ваше письмо отправлено! Спасибо.</p>
      </div>
    </div>
  </div>
  </div>
</template>

<script>
import Header from "@/components/Header";
export default {
  components: {Header},
  layout: "post_detail",
  name: "success",
  data() {
    return {
      title: "Спасибо за обращение"
    }
  }
}
</script>

<style scoped>

</style>
