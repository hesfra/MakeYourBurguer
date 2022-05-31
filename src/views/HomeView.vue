<template>
  <Banner/>
  <div class="main-container">
    <h1>Monte o seu Burguer:</h1>
    <burguerForm/>
  </div>
</template>

<script>
import Banner from "../components/Banner.vue";
import burguerForm from "../components/burguerForm.vue";
export default {
name: "Home",
components: {
  Banner,
  burguerForm
}
}
</script>

<style>

</style>