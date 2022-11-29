<template>
<h1>CALCULAR IMC</h1>
<h3>Digite seu peso e altura para calcular seu IMC:</h3>

<div class="div-imc">
  <span class="p-float-label">
    <InputText id="input-weight" type="text" v-model="weight" :disabled="imc"/>
    <label for="input-weight">Peso em Kg</label>
  </span>
</div>

<div class="div-imc">
  <span class="p-float-label">
    <InputText id="input-height" type="text" v-model="height" :disabled="imc"/>
    <label for="input-height">Altura em metros (.)</label>
  </span>
</div>

<div class="div-imc" v-if="!imc">
  <Button label="Calcular" @click="calculate" />
  <Button label="Limpar" @click="clear" class="button-calculate"/>
</div>

<div v-if="imc">
  <p class="label-result"> Seu IMC é: {{imc}}</p>
  <p>A classificação do seu IMC é: {{classification}}</p>
  <Button label="Calcular Novamente" @click="clear"/>
</div>

</template>

<script>
export default {
  data() {
    return { 
      height: null,
      weight: null,
      imc: null,
      classification:''
    }
  },
  methods: {
    calculate: function() {
      this.imc = (this.weight / (this.height * this.height)).toFixed(2);
      if(this.imc < 18.5){
      this.classification ="Magreza";
      } else if(this.imc>=18.5 && this.imc <25){
        this.classification="Normal";
      } else if (this.imc>=25 && this.imc<30){
        this.classification="Sobrepeso";
      } else if (this.imc>=30 && this.imc<40){
        this.classification="Obesidade";
      } else {
        this.classification="Obesidade Grave";
      }
      },
      clear(){
        this.height= null;
        this.weight= null;
        this.imc=null;
        this.classification='';
  
      }
      }

      }
</script>

<style>
body{
  background-color: black;
  padding-left: 10%;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #fefefe;
  
  border-radius: 10%;
  
}

.div-imc{
  margin-top: 2rem;
  
}

.label-result{
  font-size: 2rem;
}

.button-calculate{
  margin-left: 1rem !important;
}

</style>
