<template>
  <div>
    <SearchHeader @searchPosts="posts = $event"/>
    <div class="container">
      <div class="row">
        <div class="col-lg-12">
          <nav aria-label="breadcrumb" class="mt-4">
            <ol class="breadcrumb">
              <li class="breadcrumb-item"><nuxt-link to="/">Главная</nuxt-link></li>
              <li class="breadcrumb-item active" aria-current="page">Поиск</li>
            </ol>
          </nav>
          <p class="lead">Найдено записей: {{posts.count}}</p>
          <div v-for="post in posts.results" :key="post.id">
            <nuxt-link :to="`/posts/${post.slug}`"><h2>{{ post.h1 }}</h2></nuxt-link>
            <p v-html="post.description"></p>
            <hr>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import SearchHeader from "@/components/SearchHeader";
import axios from "axios";
export default {
  components: {SearchHeader},
  layout: "post_detail",
  watchQuery: ['q'],
  data() {
    return {
      posts: ''
    }
  },
  async asyncData({route}) {
    const { data } = await axios.get(`http://localhost:8000/api/posts/?search=${route.query.q}`);
    return {
      posts: data,
    }
  },
}
</script>

<style scoped>

</style>
