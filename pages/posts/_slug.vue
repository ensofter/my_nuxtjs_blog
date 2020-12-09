<template>
  <div>
    <h1>{{ post.h1 }}</h1>
  </div>
</template>

<script>
import axios from "axios";

export default {
  async asyncData({params}) {
    const post = await axios.get(`http://127.0.0.1:8000/api/posts/${params.slug}`);
    return {
      post: post.data,
    }
  },
}
</script>

<style scoped>

</style>
