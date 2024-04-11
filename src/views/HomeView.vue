<template>
  <div class="main-container">
    <banner />
    <main>
      <img id="divisa" src="/img/divisa.png" alt="Divisória">
      <section>
        <h1>Crie o seu Lanche</h1>
        <FormBurg />
      </section>
    </main>
    <img id="divisa" src="/img/divisa2.png" alt="Divisória">
  </div>
</template>

<script>
import FormBurg from '../components/FormBurg.vue';
import Banner from '../components/Banner.vue'

export default {
  name: 'HomeView',

  components: {
    Banner,
    FormBurg
  },
}
</script>

<style scoped>

#divisa {
  max-width: 100%;
}

main {
  background-color: #000;
  color: #FFF;
  margin: 0;
  padding: 0;
}

section {
  padding: 50px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 20px;
}

section h1 {
  font-size: 40px;
  color: #E4E2DD;
  text-transform: uppercase;
  text-align: center;
  margin-bottom: 20px;
}
</style>
