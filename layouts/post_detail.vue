<template>
  <div>
    <Navbar />
    <Header />
    <Nuxt />
    <Footer />
  </div>
</template>


<script>
import Navbar from "~/components/Navbar";
import Header from "~/components/Header";
import Footer from "~/components/Footer";

export default {
  components: {
    Footer,
    Header,
    Navbar,
  }
};
</script>

<style>

</style>
