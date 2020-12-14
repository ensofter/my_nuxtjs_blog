<template>
  <div>
  <h1>Привет, это страница контактов</h1>
  {{tags}}
  </div>
</template>

<script>
import axios from "axios";

export default {
  async asyncData({params}) {
    const tags = await axios.get(`http://127.0.0.1:8000/api/tags`);
    return {
      tags: tags.data
    }
  },
}
</script>

<style scoped>

</style>
