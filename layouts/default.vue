<template>
  <div>
    <Navbar />
    <Slider />
      <Nuxt />
    <Footer />
  </div>
</template>


<script>
import Navbar from "~/components/Navbar";
import Slider from "~/components/Slider";
import Footer from "~/components/Footer";

export default {
    components: {
    Footer,
    Slider,
    Navbar,
  },
  head() {
    return {
      link: [
        { rel: "canonical", href: `http://localhost:3000${this.$route.path}`}
      ]
    }
  },
};
</script>

<style>

</style>
