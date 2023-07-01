<template>
  <div>
    <div>
      <form id="burger-form" method="POST" @submit="createPizza">
        <div class="input-container">
          <label for="nome">Nome do cliente: {{ nome }}</label>
          <input
            type="text"
            id="nome"
            name="nome"
            v-model="nome"
            placeholder="Digite o seu nome"
          />
        </div>
        <div class="input-container">
          <label for="telefone">Telefone do cliente: {{ telefone }}</label>
          <input
            type="text"
            id="telefone"
            name="telefone"
            v-model="telefone"
            placeholder="Digite o seu telefone"
          />
        </div>
        <div class="input-container">
          <label for="endereco">Endereço do cliente: {{ endereco }}</label>
          <input
            type="text"
            id="endereco"
            name="endereco"
            v-model="endereco"
            placeholder="Digite o seu endereço"
          />
        </div>
        <div class="input-container">
          <label for="tamanho">Tamanho pizza: {{ tamanho }}</label>
          <select name="tamanho" id="tamanho" v-model="tamanho">
            <option value="Selecione o tamanho">Selecione o tamanho</option>
            <option value="Grande">Grande</option>
            <option value="Média">Média</option>
            <option value="Pequena">Pequena</option>
          </select>
        </div>
        <div id="opcionais-container" class="input-container">
          <label id="sabores" for="sabores"> Selecione os sabores: </label>
          <div
            v-for="(opcional, index) in optionSabores"
            :key="index"
            class="checkbox-container"
          >
            <input
              type="checkbox"
              name="sabores"
              v-model="sabores"
              :value="opcional.nome"
            />
            <span>{{ opcional.nome }}</span>
          </div>
        </div>

        <div class="input-container">
          <label for="telefone">Observações: {{ Observacoes }}</label>
          <textarea
            type="text"
            id="telefone"
            name="Observacoes"
            v-model="Observacoes"
            placeholder="Digite suas Observações"
          ></textarea>
        </div>
        <div class="input-container">
          <input class="submit-btn" type="submit" value="Enviar meu pedido!" />
        </div>
      </form>
    </div>
  </div>
</template>
  
  <script>
import Swal from "sweetalert2";

export default {
  name: "BurgerForm",
  data() {
    return {
      nome: null,
      telefone: null,
      endereco: null,
      tamanho: null,
      sabores: [],
      Observacoes: null,
      id: Math.floor(Math.random() * 1000),
      optionSabores: null,
    };
  },

  methods: {
    async createPizza(e) {
      e.preventDefault();

      const data = {
        id: this.id,
        nome: this.nome,
        telefone: this.telefone,
        endereco: this.endereco,
        tamanho: this.tamanho,
        sabores: Array.from(this.sabores),
        observacoes: this.Observacoes,
        data: new Date().toISOString().split("T")[0],
      };

      const dataJson = JSON.stringify(data);

      const req = await fetch(" http://localhost:3000  /pedidos", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: dataJson,
      });

      const res = await req.json();

      console.log("Pedido realizado com sucesso!" + res);

      Swal.fire({
        icon: "success",
        title: "Pedido realizado!",
      });
      // clear message
      setTimeout(() => (this.msg = ""), 3000);

      // limpar campos
      this.id = "";
      this.nome = "";
      this.telefone = "";
      this.endereco = "";
      this.tamanho = "";
      this.sabores = [];
      this.Observacoes = "";
    },
  },

  mounted() {
    (async () => {
      const req = await fetch(" http://localhost:3000  /banco2");
      const data = await req.json();

      this.optionSabores = data.sabores;
      console.log(data.sabores);
    })();
  },

  components: {},
};
</script>
  
  <style scoped>
#burger-form {
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
  border-left: 4px solid #ff1717;
}

input,
select,
textarea {
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