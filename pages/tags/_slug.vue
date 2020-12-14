<template>
  <div>
    <p>{{ posts }}</p>
  </div>
</template>

<script>
import axios from "axios";


export default {
  layout: "post_detail",
  async asyncData({params}) {
    const post = await axios.get(`http://127.0.0.1:8000/api/tags/${params.slug}`);
    return {
      posts: post.data,
    }
  },
}
</script>

<style scoped>

</style>
