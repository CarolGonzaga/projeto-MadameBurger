<template>
  <div class="message-container">
      <p>{{ msg }}</p>
  </div>
</template>

<script>
export default {
    name: "Message",

    props: {
        msg: String
    }
}
</script>

<style scoped>
    .message-container {
        color: #000;
        background-color: #F0D3AD;
        border: 2px solid #917f68;
        border-radius: 5px;
        padding: 5px;
        max-width: 400px;
        margin: 30px auto;
    }

    p {
        border: 2px solid #917f686b;
        border-style: dotted;
        padding: 10px;
    }
</style>