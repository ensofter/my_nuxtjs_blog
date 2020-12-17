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
          <p class="lead">Чтобы связаться со мной заполните форму обратной связи</p>
          <form name="contact-form">
            <div class="row">
              <div class="col-md-6">
                <div class="md-form mb-0">
                  <label for="name" class="sr-only">Ваше имя</label>
                  <input type="text" id="name" class="form-control" placeholder="Ваше имя" v-model="form.name" >
                </div>
              </div>
              <div class="col-md-6">
                <div class="md-form mb-0">
                  <label for="email" class="sr-only">Ваша почта</label>
                  <input type="text" id="email" class="form-control" placeholder="Ваша почта" v-model="form.email" >
                </div>
              </div>
            </div>

            <div class="row mt-3">
              <div class="col-md-12">
                <div class="md-form mb-0">
                  <label for="subject" class="sr-only">Тема</label>
                  <input type="text" id="subject" class="form-control" placeholder="Тема" v-model="form.subject" >
                </div>
              </div>
            </div>

            <div class="row mt-3">
              <div class="col-md-12">
                <div class="md-form">
                  <label for="message" class="sr-only">Ваше сообщение</label>
                  <textarea type="text" id="message" rows="2" class="form-control md-textarea" placeholder="Ваше сообщение" v-model="form.message" ></textarea>
                </div>
              </div>
            </div>
          </form>
          <div class="text-center text-md-left mt-3">
            <button class="btn btn-primary" type="submit" @click.prevent="submitForm" :disabled='!isComplete'>Отправить</button>
          </div>
          </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Header from "@/components/Header";

export default {
  components: {Header},
  layout: "post_detail",
  data() {
    return {
      title: "Написать мне",
      form: {
        name: '',
        email: '',
        subject: '',
        message: '',
      }
      }
    },
    methods: {
      submitForm() {
        let contactFormData = new FormData();
        contactFormData.set('name', this.form.name);
        contactFormData.set('email', this.form.email);
        contactFormData.set('subject', this.form.subject);
        contactFormData.set('message', this.form.message);
        axios({
          method: 'post',
          url: 'http://localhost:8000/api/feedback/',
          data: contactFormData
        }).then(function (response) {
          console.log(response);
        }).catch(function (response) {
          console.log(response);
        });
        this.$router.push("/success");
      }
    },
    computed: {
      isComplete () {
        return this.form.name && this.form.email && this.form.subject && this.form.message;
      }
    }
  }
  </script>

<style scoped>

</style>
