<template>
<div class="wrapper">
	<div v-for="burger in burgers" :key="burger.id" class="lista-item">
   
		<input class="trigger-input"  :id="'faq-titulo-' + burger.id"  type="checkbox">
		<div class="trigger-wrapper">
			<label :for="'faq-titulo-' + burger.id">
				<h2 class="faq-titulo">{{ burger.nome }}</h2>
			</label>
      <ul class="faq-conteudo" v-for="(opcional, index) in burger.sabores" :key="index">
            <li><b>Sabor - {{ index+1 }}:</b> {{ opcional }}</li>
      </ul>
      <p class="faq-conteudo"><b>Tamanho: </b>{{ burger.tamanho }}</p>
			<p class="faq-conteudo"><b>Observações: </b>{{ burger.observacoes }}</p>
			<p class="faq-conteudo"><b>Data: </b>{{ burger.data }}</p>
			<p class="faq-conteudo"><b>Telefone: </b>{{ burger.telefone }}</p>
			<p class="faq-conteudo"><b>Endereço: </b>{{ burger.endereco }}</p>
      <center>
      <button class="delete-btn - faq-conteudo" @click="deletePizza(burger.id)">Finalizado!</button>
    </center>
		</div>
	</div>
	

</div>
</template>
<script>
  export default {
    name: "Dashboard",
    data() {
      return {
        burgers: null,
        burger_id: null,
        status: []
      }
    },
    methods: {
      async getPedidos() {
        const req = await fetch(' http://localhost:3000  /pedidos')

        const data = await req.json()

        this.burgers = data


      },
      async deletePizza(id) {

        const req = await fetch(` http://localhost:3000  /pedidos/${id}`, {
          method: "DELETE"
        });

        const res = await req.json()

        this.getPedidos()

      },
      async updateBurger(event, id) {

        const option = event.target.value;

        const dataJson = JSON.stringify({status: option});

        const req = await fetch(` http://localhost:3000  /burgers/${id}`, {
          method: "PATCH",
          headers: { "Content-Type" : "application/json" },
          body: dataJson
        });

        const res = await req.json()

        console.log(res)

      }
    },
    mounted () {
    this.getPedidos()
    }
  }
</script>

<style scoped>


.wrapper {
	max-width: 400px;
	margin: 0 auto;
}


.lista-item {
	background: #ffffff;
	border-radius: 4px;
	margin-bottom: 20px;
	padding: 10px;
	box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
  border-bottom: 1px solid  #111;
}

.faq-titulo {
	cursor: pointer;
	padding: 10px;
	font-size: 1.4em;
	font-family: monospace;
	color: #292929;
}

.faq-titulo::before {
	content: "";
	display: inline-block;
	height: 12px;
	width: 24px;
	margin-right: 10px;
	background: #ff0000;
}

.faq-titulo::after {
	content: "+";
	float: right;
	transition: transform 0.3s ease;
}

.faq-conteudo {
	padding: 10px;
	color: #6b7c93;
	font-family: Helvetica;
	font-size: 0.875em;
	line-height: 1.4em;
	display: none;
}

.trigger-input {
	display: none;
}

.trigger-input:checked + .trigger-wrapper .faq-conteudo {
	display: block;
}

.trigger-input:checked + .trigger-wrapper .faq-titulo::after {
	transform: rotate(45deg) scale(1.08);
}

  #burger-table {
    max-width: 1200px;
    margin: 0 auto;
  }

  #burger-table-heading,
  #burger-table-rows,
  .burger-table-row {
    display: flex;
    flex-wrap: wrap;
  }

  #burger-table-heading {
    font-weight: bold;
    padding: 12px;
    border-bottom: 3px solid #333;
  }

  .burger-table-row {
    width: 100%;
    padding: 12px;
    border-bottom: 1px solid #CCC;
  }

  #burger-table-heading div,
  .burger-table-row div {
    width: 19%;
  }

  #burger-table-heading .order-id,
  .burger-table-row .order-number {
    width: 5%;
  }

  select {
    padding: 12px 6px;
    margin-right: 12px;
  }

  .delete-btn {
    background-color: #222;
    color:#fcba03;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
  }
  
  .delete-btn:hover {
    background-color: transparent;
    color: #222;
  }
  
</style>