<template>
  <div class="container">
      <slot />
    <div class="board">
      <div class="valores">
        <h1>{{ primeiroValor }} x {{ segundoValor }}</h1>
        <input type="number" v-model="valor" />
      </div>
      <div class="result">
        <div class="val-result">
          <span v-if="message == 'CORRETA'" class=""
            >A resposta esta: <span class="acerto">{{ message }}</span></span
          >
          <span v-else
            >A resposta esta: <span class="erro">{{ message }}</span></span
          >
        </div>

        <div class="respo">
          <button @click="calcular" class="btn">Responder</button>
        </div>
        <div class="detalhes">
          <span><i class="fas fa-check"></i> Acertos: {{ corretas }}</span>
          <span> <i class="fas fa-times"></i> Erros: {{ erradas }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      valor: 0,
      erros: [],
      acertos: [],
      primeiroValor: 0,
      segundoValor: 0,
      correta: false,
      message: '',
    };
  },
  created() {
    this.gerarValoresAleatorios();
  },
  methods: {
    gerarValoresAleatorios() {
      this.primeiroValor = Math.floor(Math.random() * 10);
      this.segundoValor = Math.floor(Math.random() * 10);
    },
    calcular() {
      this.valor == this.primeiroValor * this.segundoValor
        ? this.correto()
        : this.errado();

      this.gerarValoresAleatorios();
      this.valor = '';
    },
    correto() {
      this.acertos.push(this.primeiroValor * this.segundoValor);
      this.message = "CORRETA";
    },
    errado() {
      this.erros.push(this.primeiroValor * this.segundoValor);
      this.message = "ERRADA";
    },
  },
  computed: {
    corretas: function () {
      return this.acertos.length;
    },
    erradas: function () {
      return this.erros.length;
    },
  },
};
</script>

<style lang="css" scoped>
.container{
  background-color: rgb(151 151 151 / 10%);
  display: flex;
  align-items: center;
  justify-content: center;
  height: auto;
  padding: 1.5em;
  flex-direction: column;
  position: relative;
  height: 100vh;
  border: 1px solid;
}
.board {
  padding: 1.5em;
  margin: 0.7em 0;
  padding: 1em;
  background: transparent;
  outline: none;
  border: 3px solid rgba(255, 255, 255, 0.2);
  border-radius: 10px;

  box-shadow: 2px 2px 2px rgba(0, 0, 0, 0.08),
    -3px -2px 3px rgba(255, 255, 255, 0.2),
    2px 2px 2px rgba(0, 0, 0, 0.08) inset;
}
.valores {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: center;
}
.valores h1 {
  color: rgba(0, 0, 0, 0.7);
}
.valores h1,
input {
  margin: 0 5px;
}
.result {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
  text-align: center;
}
.respo {
  margin-bottom: 10px;
  margin-top: 10px;
}
.detalhes span {
  margin: 0 5px;
}
input {
  margin: 0.7em 0;
  padding: 1em;
  background: transparent;
  outline: none;
  border: 3px solid rgba(255, 255, 255, 0.2);
  border-radius: 10px;

  box-shadow: 2px 2px 2px rgba(0, 0, 0, 0.08),
    -3px -2px 3px rgba(255, 255, 255, 0.2),
    2px 2px 2px rgba(0, 0, 0, 0.08) inset;
}
.btn {
  margin: 10px 0;
  border: none;
  font-size: 1em;
  background-color: transparent;
  padding: 1em;
  border-radius: 10px;
  color: #787878;
  cursor: pointer;
  outline: none;
  text-shadow: 1px 1px 0 rgba(255, 255, 255, 0.4);
  transition: box-shadow ease 250ms;
  border-bottom: 1px solid rgba(255, 255, 255, 0.3);
  border-right: 1px solid rgba(255, 255, 255, 0.3);

  box-shadow: -6px -6px 16px rgba(255, 255, 255, 0.6),
    6px 6px 16px rgba(0, 0, 0, 0.2);
}
.btn:hover {
  box-shadow: -6px -6px 8px rgba(255, 255, 255, 0.6),
    6px 6px 8px rgba(0, 0, 0, 0.2);
}
.btn:active {
  box-shadow: -6px -6px 8px rgba(255, 255, 255, 0), 6px 6px 8px rgba(0, 0, 0, 0),
    inset -6px -6px 8px rgba(255, 255, 255, 0.6),
    inset 6px 6px 8px rgba(0, 0, 0, 0.2);
}
.erro {
  color: rgb(228, 77, 77);
}
.acerto {
  color: rgb(40, 202, 40);
}
.fa-check {
  color: rgb(40, 202, 40);
}
.fa-times {
  color: rgb(228, 77, 77);
}
</style>
