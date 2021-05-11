<template>
  <div class="container">
      <slot />

    <div class="board">
      <div class="vidas">
        <div class="text-vidas">
          <span>Chances</span>
        </div>
        <div class="coracoes">
        <i :class="[{fas: vidas[index].valor},far]" class="fa-heart" v-for="(value, index) in vidas" :key="index" ></i>
        </div>
      </div>
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
          <button @click="calcular" class="btn" v-if="!fimDeJogo">Responder</button>
          <button @click="reiniciar" class="btn" v-else>Reiniciar</button>
        </div>
        <div class="detalhes" v-if="fimDeJogo">
          <div class="pontuacao">
            <span>Você fez {{pontuacao}} pontos!</span>
          </div>
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
      fimDeJogo: false,
      valor: 0,
      current: 0,
      erros: [],
      acertos: [],
      primeiroValor: 0,
      segundoValor: 0,
      correta: false,
      message: '',
      vidas: [ {class: 'fas', valor: true},  {class: 'fas', valor: true},  {class: 'fas', valor: true},  {class: 'fas', valor: true},  {class: 'fas', valor: true},  {class: 'fas', valor: true},  {class: 'fas', valor: true}],
      temVidas: true,
      far: 'far',
      pontuacao: 0,
    };
  },
  created() {
    this.gerarValoresAleatorios();
  },
  methods: {
    gerarValoresAleatorios() {
      this.primeiroValor = Math.floor(Math.random() * 15);
      this.segundoValor = Math.floor(Math.random() * 14);
    },
    calcular() {
      
      +this.valor === +this.primeiroValor * +this.segundoValor
        ? this.correto()
        : this.errado();
      this.gerarValoresAleatorios();
      this.valor = '';
    },
    correto() {
      this.acertos.push(this.primeiroValor * this.segundoValor);
      this.message = "CORRETA";
      this.pontuacao += 10;
    },
    errado() {
      this.erros.push(this.primeiroValor * this.segundoValor);
      this.message = "ERRADA";

      if(this.current < this.vidas.length){

        this.vidas[this.current].class = 'far'
        this.vidas[this.current].valor = false
        this.current++
      }else{
        this.fimDeJogo = true;
      }
    },
    reiniciar(){
      this.fimDeJogo = false;
      this.current = 0;
      this.message = ''
      this.vidas.forEach(v => {
        v.valor = true;
        v.class = 'fas'
      })
    }
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
.vidas{
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
}
.coracoes{
  display: flex;
  margin-top: .2em;
}
.coracoes i{
  margin: 0 2px;
}
.vidas i{
  color: rgb(228, 77, 77);
}
.text-vidas{
  font-size: .8em;
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
.pontuacao{
  margin-bottom: .2em;
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
