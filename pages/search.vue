<template>
  <div>
    <Search />
    <div class="container">
      <div class="row">
        <div class="col-lg-12">
          <nav aria-label="breadcrumb" class="mt-4">
            <ol class="breadcrumb">
              <li class="breadcrumb-item"><nuxt-link to="/">Главная</nuxt-link></li>
              <li class="breadcrumb-item active" aria-current="page">Поиск</li>
            </ol>
          </nav>
          <p class="lead">Найдено записей: 1</p>
          {{posts}}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Search from "@/components/Search";
import axios from "axios";
export default {
  components: {Search},
  layout: "post_detail",
  name: "search",
  data() {
    return {
      title: "Спасибо за обращение"
    }
  },
  async asyncData({route}) {
    const { data } = await axios.get(`http://localhost:8000/api/posts/?search=${route.query.q}`);
    return {
      posts: data.results,
    }
  },
}
</script>

<style scoped>

</style>
