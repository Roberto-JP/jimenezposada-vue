<template>
  <div id="app">
    <h1 Class="title">Roberto David Jimenez Posada</h1>
    <h2>Aplicacion de calculadora</h2>
    <div class="calculator">
      <input type="text" class="result" :value="result" readonly>
      <div class="buttons"> 
        <button class="number" @click="handleClick('7')">7</button>
        <button class="number" @click="handleClick('8')">8</button>
        <button class="number" @click="handleClick('9')">9</button>
        <button class=" operator" @click="handleOperatorClick('/')">/</button>

        <button class="number" @click="handleClick('7')">4</button>
        <button class="number" @click="handleClick('8')">5</button>
        <button class="number" @click="handleClick('9')">6</button>
        <button class=" operator" @click="handleOperatorClick('*')">*</button>

        <button class="number" @click="handleClick('7')">1</button>
        <button class="number" @click="handleClick('8')">2</button>
        <button class="number" @click="handleClick('9')">3</button>
        <button class=" operator" @click="handleOperatorClick('-')">-</button>

        <button class="number" @click="handleClick('7')">0</button>
        <button class="number" @click="handleClick('8')">.</button>
        <button class="number" @click="handleClick('9')">00</button>
        <button class=" operator" @click="handleOperatorClick('+')">+</button>

    </div>
    </div>
  </div>
  
</template>

<script>
 export default{
  name:'App',
  data(){
    return{
      result:'',
      calculated: false
    };

  },
  methods: {
    handleClick(value){
      if(this.calculated){
        this.result = value;
        this.calculated = false;
      }else{
        this.result +=value;
      }
    },
    handleClear(){
      this.result = '';
      this.calculated  = false;
    },
    handleClearEntry(){
      if(this.result && this.result.length > 0){
        this.result = this.result.slicer(0,-1);
        if(this.result.length === 0){
          this.handleClear();
        }
    }else{
      this.handleClear();
    }
  },
handleOperatorClick(operator){
if(/[+*/-]$/.test(this.result) ){
  this.result = this.result.slice(0,-1)+operator;
}else{
  this.result += operator;
}
this.calculated = false;
},
calculate(){
  try{
    let evaluateResult = eval(this.result.replace(/(^|[0-9])0+(d+)/g,'$1$2'));
    if(evaluateResult === Infinity || evaluateResult === -Infinity){
      throw new Error('Dividion por cero');
    }
    this.result = Number.isFinite(evaluateResult) ? evaluateResult : 'Error' ;
  }catch(error){
    if(error.message == 'División por cero'){
      this.result = 'Error: División por cero';
    }else{
      this.error = 'Error';
    }
  }
}
},
}
</script>
<style  src="./calculadora.css">


</style>
