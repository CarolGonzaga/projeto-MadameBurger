<template>
  <header>
    <h1>Monte do seu jeito</h1>
    <img src="/img/burguer.png" alt="Hamburguer">
  </header>
</template>

<script>
export default {
  name: 'Banner'
}
</script>

<style scoped>
  header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin: 50px;
  }

  header img {
    height: 370px;
  }

  header h1 {
    font-size: 85px;
    text-transform: uppercase;
    color: #B82E29;
    max-width: 590px;
    text-align: center;
  }

  @media (max-width: 1000px) {
    header img {
    height: 300px;
  }

  header h1 {
    font-size: 50px;
    text-transform: uppercase;
    color: #B82E29;
    max-width: 400px;
    text-align: center;
  }
  }

  @media (max-width: 600px) {
    header img {
    height: 200px;
  }

  header h1 {
    font-size: 50px;
    text-transform: uppercase;
    color: #B82E29;
    max-width: 300px;
    text-align: center;
  }
  }

  @media (max-width: 500px) {
    header {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
    margin: 50px;
    gap: 30px;
    }
  }
</style>