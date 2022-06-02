<script>
import Navbar from './components/Navbar.vue';
import { RouterView } from 'vue-router';
import Footer from './components/footer.vue';


export default {
  components: {
    Navbar,
    RouterView,
    Footer,
  },
  data() {
    return {
      logo_src: "/img/logo.png",
      app_name: "Make Your Burger",
    }
  }

}

</script>

<template>
  <div>
    <Navbar :logo="logo_src" :alt="app_name" />
    <div>
      <router-view></router-view>
    </div>
    <Footer />
  </div>
</template>

<style>
* {
  font-family: Helvetica;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.mainContainer {
  margin: 50px;
  min-height: 250px;
  margin-top: 100px;
  padding-bottom: 25%;
  
}

h1 {
  text-align: center;
  font-size: 42px;
  margin-bottom: 30px;
  color: #222;
}
</style>
