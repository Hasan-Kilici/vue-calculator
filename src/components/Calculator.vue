<template>

  <div class="p-3" style="max-width: 400px; margin: 50px auto; background: #234">
    

    <div class="input">
      {{ calculatorValue || 0 }}
    </div>


    <div class="row">
      <div class="col-3" v-for="n in calculatorElements" :key="n">
        <div class="btn lead text-white text-center m-1 py-3 bg-vue-dark rounded hover-class"
          :class="{'bg-vue-green': ['C','*','/','-','+','%','='].includes(n)}"
          @click="action(n)">
          {{n}}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Calculator',
  props: {
    msg: String
  },

  data() {
    return {
      calculatorValue: '',
      calculatorElements: ['C','*','/','-',7,8,9,'+',4,5,6,'%',1,2,3,'=',0,'.'],
      operator: null,
      previousCalculatorValue: '',
    }
  },

  methods: {
    action(n){

      /* Append value */
      if(!isNaN(n) || n === '.'){
        this.calculatorValue += n + '';
      }

      /* Clear value */
      if(n === 'C'){
        this.calculatorValue = '';
      }

      /* Percentage */
      if(n === '%'){
        this.calculatorValue = this.calculatorValue / 100 + '';
      }

      /* Operators */
      if(['/','*','-','+'].includes(n)){
        this.operator = n;
        this.previousCalculatorValue = this.calculatorValue;
        this.calculatorValue = '';
      }

      /* Calculate result using the eval function */
      if(n === '='){
        this.calculatorValue = eval(
          this.previousCalculatorValue + this.operator + this.calculatorValue
        );
        this.previousCalculatorValue = '';
        this.operator = null;
      }
    }
  }
}
</script>


<style scoped>
  .bg-vue-dark {
    background: #31475e;
  }
  .hover-class:hover {
    cursor: pointer;
    background: #3D5875;
  }
  .bg-vue-green {
    background: #3fb984;
  }
  .row{
    display:flex;
    flex-direction:row;
    flex-wrap:wrap;
    gap:10px;
  }
  .col-3{
    width:18%;
    padding:10px;
  }
  .btn{
    padding-top:20px;
    padding-bottom:20px;
    text-align:center;
    color:white;
    border-radius:8px;
  }
  .input{
    background: #31475e;
    padding:10px;
    max-width:400px;
    color:white;
    border:10px solid #234;
    border-radius:16px;
    margin-top:-10px;
  }
</style>
