<template>
  <div>
    <div>
      <form id="burger-form" @submit="createBurger">

        <!-- Campo de entrada para o nome do cliente -->
        <div class="input-container">
          <label for="name">Cliente:</label>
          <input type="text" id="name" name="name" v-model="name" placeholder="Digite o seu nome">
        </div>

        <!-- Campo de seleção para o tipo de pão -->
        <div class="input-container">
          <label for="bread">Selecione o Pão:</label>
          <select name="bread" id="bread" v-model="bread">
            <option v-for="breadForm in breadBack" :key="breadForm.id" :value="breadForm.tipo">
              {{ breadForm.tipo }}
            </option>
          </select>
        </div>

        <!-- Campo de seleção para o tipo de carne -->
        <div class="input-container">
          <label for="meat">Selecione a Carne:</label>
          <select name="meat" id="meat" v-model="meat">
            <option v-for="meatForm in meatBack" :key="meatForm.id" :value="meatForm.tipo">
              {{ meatForm.tipo }}
            </option>
          </select>
        </div>

        <!-- Campo de seleção para o tipo de molho -->
        <div class="input-container">
          <label for="sauce">Selecione o Molho:</label>
          <select name="sauce" id="sauce" v-model="sauce">
            <option v-for="sauceForm in sauceBack" :key="sauceForm.id" :value="sauceForm.tipo">
              {{ sauceForm.tipo }}
            </option>
          </select>
        </div>

        <!-- Campo de seleção para os opcionais -->
        <div class="input-container" id="opt-container">
          <label id="opt-title" for="opcionais">Selecione os Opicionais:</label>
          <div class="check-container" v-for="opicional in opicionaisdata" :key="opicional.id">
            <input type="checkbox" name="opicionais" v-model="opicionais" :value="opicional.tipo">
            <span>{{ opicional.tipo }}</span>
          </div>
        </div>

        <!-- Botão de envio do pedido -->
        <div class="input-container">
          <input type="submit" class="submit-btn" value="Enviar Pedido">
        </div>

        <!-- Componente de Mensagem -->
        <Message :msg="msg" v-show="msg" />

      </form>
    </div>
  </div>
</template>

<script>
import Message from './Message.vue';

export default {
  name: 'FormBurg',

  components: {
    Message
  },

  data() {
    return {
      // Dados vindos do servidor
      breadBack: null,
      meatBack: null,
      sauceBack: null,
      opicionaisdata: null,

      // Dados do formulário
      name: null,
      bread: null,
      meat: null,
      sauce: null,
      opicionais: [],

      // Mensagem de resposta do servidor
      msg: null
    }
  },

  methods: {
    // Método para obter os ingredientes do servidor
    async getIngredients() {
      try {
        const req = await fetch("https://api-madameburger-bay.vercel.app/ingredientes");
        const data = await req.json();
        console.log(data); // Verificar os dados recebidos no console
        this.breadBack = data.paes;
        this.meatBack = data.carnes;
        this.sauceBack = data.molhos;
        this.opicionaisdata = data.opcionais;
      } catch (error) {
        console.error("Erro ao obter os ingredientes:", error);
      }
    },

    // Método para criar um novo pedido de hambúrguer
    async createBurger(e) {
      e.preventDefault();

      // Construindo o objeto de dados a ser enviado ao servidor
      const data = {
        nome: this.name,
        pao: this.bread,
        carne: this.meat,
        molho: this.sauce,
        extras: Array.from(this.opicionais),
        status: "Aberto"
      }

      // Convertendo os dados para JSON
      const dataJson = JSON.stringify(data);

      // Enviando os dados para o servidor via POST
      const req = await fetch("https://api-madameburger-bay.vercel.app/burgers", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: dataJson
      });

      // Recebendo a resposta do servidor
      const res = await req.json();

      // Enviando uma mensagem ao usuário
      this.msg = `Pedido nº ${res.id}, realizado com sucesso!`

      // Limpar mensagem da tela
      setTimeout(() => this.msg = "", 3000);

      // Limpar campos do formulário após o envio bem-sucedido
      this.name = "";
      this.bread = "";
      this.meat = "";
      this.sauce = "";
      this.opicionais = "";
    }
  },

  // Método executado após a montagem do componente
  mounted() {
    this.getIngredients()
  }
}
</script>

<style scoped>
#burger-form {
  max-width: 400px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.input-container {
  display: flex;
  flex-direction: column;
  margin-bottom: 30px;
}

label {
  font-weight: bold;
  margin-bottom: 10px;
  color: #FFF;
  padding: 5px 10px;
  border-left: 4px solid #B82E29;
}

input,
select {
  padding: 5px 10px;
  width: 300px;
}

#opt-container {
  display: grid;
  grid-template-columns: 2fr 1fr;
  width: 300px;
}

#opt-title {
  width: 100%;
  margin-bottom: 20px;
  grid-column: span 2;
}

.check-container {
  display: flex;
  align-items: center;
  margin-bottom: 20px;
}

.check-container input {
  width: auto;
}

.check-container span {
  margin-left: 6px;
  font-weight: bold;
  font-size: 12px;
}

.submit-btn {
  background-color: #B82E29;
  color: #E4E2DD;
  font-weight: bold;
  border: 2px solid #B82E29;
  padding: 10px;
  font-size: 16px;
  margin: 0 auto;
  cursor: pointer;
  transition: .5s;
}

.submit-btn:hover {
  background-color: transparent;
  color: #B82E29;
}
</style>
