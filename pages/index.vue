<template>
  <div class="container">
    <h1 class="my-3">Последние записи блога</h1>
    <div class="row">
      <div v-for="post in posts" :key="post.slug" class="col-md-4">
          <div class="card mb-4 shadow-sm">
            <img :src="post.image" alt="" class="card-img-top">
            <div class="card-body">
              <h4 class="card-title">{{ post.h1 }}</h4>
              <div v-html="post.description" class="truncate"></div>
              <div class="mb-2">
              <span v-for="tag in post.tags">
                <nuxt-link :to="`/tags/${tag}`" class="mr-1 badge badge-info">#{{ tag }}</nuxt-link>
              </span>
              </div>
              <div class="d-flex justify-content-between align-items-center">
                <div class="btn-group">
                  <nuxt-link :to="`/posts/${post.slug}`" class="btn btn-sm btn-outline-secondary">Подробнее</nuxt-link>
                </div>
                <small class="text-muted">{{ post.created_at }}</small>
              </div>
            </div>
          </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Default from "@/layouts/default";
export default {
  components: {Default},
  async asyncData(ctx) {
    const { data } = await axios.get(`http://127.0.0.1:8000/api/posts/`);
    return {
      posts: data.results,
    }
  },
}
</script>

<style>

</style>
