<template>
  <div>
    <Navbar :logo="logo_src" :alt="app_name" />
    <router-view />
    <Footer />
  </div>
</template>

<script>
import Navbar from './components/Navbar.vue'
import Footer from './components/Footer.vue'

export default {
  components: {
    Navbar,
    Footer
  },

  data() {
    return {
      logo_src: "/img/logo.png",
      app_name: "MadameBurguer"
    }
  }

}
</script>

<style>
* {
  font-family: 'Roboto';
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

html {
  background-color: #F0D3AD;
}

body {
  max-width: 1200px;
  margin: auto;
  background-color: #E4E2DD;
}

.main-container {
  min-height: 250px;
}

.divisa {
  max-width: 100%;
}

</style>
