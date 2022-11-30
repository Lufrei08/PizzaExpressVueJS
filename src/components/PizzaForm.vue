<template>
  <div>
    <Message :msg="msg" v-show="msg" />
    <div>
      <form id="pizzaform" @submit="mountPizza">
        <div class="input-container">
          <label for="nome">Nome do Cliente:</label>
          <input
            type="text"
            name="nome"
            id="nome"
            v-model="nome"
            placeholder="Digite seu nome"
          />
        </div>

        <div id="opcionais-container" class="input-container">
          <label id="opcionais-title" for="opcionais">Selecione o sabor:</label>
          <div class="checkbox-container" v-for="sabor in saboresdata" :key="sabor.id">
            <input
              type="checkbox"
              name="opcionais"
              v-model="opcionais"
              :value="sabor.tipo"
            />
            <span>{{ sabor.tipo }}</span>
          </div>
        </div>

        <div class="input-container">
          <label for="tamanho">Escolha o tamanho:</label>
          <select name="tamanho" id="tamanho" v-model="tamanho">
            <option value="">Selecione o tamanho</option>
            <option v-for="tamanho in tamanhos" :key="tamanho.id" :value="tamanho.tipo">
              {{ tamanho.tipo }}
            </option>
          </select>
        </div>

        <div class="input-container">
          <label for="borda">Escolha a borda:</label>
          <select name="borda" id="borda" v-model="borda">
            <option value="">Selecione a borda:</option>
            <option v-for="borda in bordas" :key="borda.id" :value="borda.tipo">
              {{ borda.tipo }}
            </option>
          </select>
        </div>

        <div class="input-container">
          <input type="submit" class="submit-btn" value="Montar minha pizza" />
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import Message from "./Message.vue";
export default {
  name: "PizzaForm",
  data() {
    return {
      saboresdata: null,
      tamanhos: null,
      bordas: null,
      nome: null,
      opcionais: [],
      tamanho: null,
      borda: null,
      status: "Solicitado",
      msg: null,
    };
  },
  methods: {
    async getIngredients() {
      const req = await fetch("http://localhost:3000/ingredientes");
      const data = await req.json();

      this.saboresdata = data.sabores;
      this.tamanhos = data.tamanhos;
      this.bordas = data.bordas;
    },

    async mountPizza(e) {
      e.preventDefault();

      const data = {
        nome: this.nome,
        sabor: Array.from(this.opcionais),
        tamanho: this.tamanho,
        borda: this.borda,
        status: "Solicitado",
      };

      const dataJson = JSON.stringify(data);

      const req = await fetch("http://localhost:3000/pizzas", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: dataJson,
      });

      const res = await req.json();

      //Mensagem de conclusão
      this.msg = `Pedido Nº ${res.id} realizado com sucesso!`;

      //Limpar mensagem
      setTimeout(() => (this.msg = ""), 4000);

      //Limpar campos após inserção
      this.nome = "";
      this.tamanho = "";
      this.borda = "";
    },
  },
  mounted() {
    this.getIngredients();
  },
  components: {
    Message,
  },
};
</script>

<style scoped>
#pizzaform {
  max-width: 400px;
  margin: 0 auto;
}

.input-container {
  display: flex;
  flex-direction: column;
  margin-bottom: 20px;
}

label {
  font-weight: bold;
  margin-bottom: 15px;
  color: #222;
  padding: 5px 10px;
  border-left: 4px solid #fcba03;
}

input,
select {
  padding: 5px 10px;
  width: 300px;
}
#opcionais-container {
  flex-direction: row;
  flex-wrap: wrap;
}
#opcionais-title {
  width: 100%;
}
.checkbox-container {
  display: flex;
  align-items: flex-start;
  width: 50%;
  margin-bottom: 20px;
}
.checkbox-container span,
.checkbox-container input {
  width: auto;
}
.checkbox-container span {
  margin-left: 6px;
  font-weight: bold;
}

.submit-btn {
  background-color: #222;
  color: #fcba03;
  font-weight: bold;
  border: 2px solid #222;
  padding: 10px;
  font-size: 16px;
  margin: 0 auto;
  cursor: pointer;
  transition: 0.5s;
}

.submit-btn:hover {
  background-color: transparent;
  color: #222;
}
</style>
