<template>
  <!-- Happy Coding -->
  <div class="p-3" style="max-width: 400px; margin: 50px auto; background: #234">
    
    <!-- Calculator Result -->
    <div class="w-full rounded m-1 p-3 text-right lead font-weight-bold text-white bg-vue-dark">
      {{ calculatorval || 0 }}
    </div>

    <!-- Calculator buttons -->
    <div class="row no-gutters">
      <div class="col-3" v-for="n in calculatorElm" :key="n">
        <div class="lead text-white text-center m-1 py-3 bg-vue-dark rounded hover-class"
          :class="{'bg-vue-green': ['C','*','/','-','+','%','='].includes(n)}"
          @click="action(n)"
        >
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
      calculatorval:'',
      calculatorElm : ['C','*','/','-',7,8,9,'+',4,5,6,'%',1,2,3,'=',0,'.'],
      operator: null,
      prevCalcul: '',
    }
  },
  methods: {
    action(n){
      if(!isNaN(n) || n === '.'){
        this.calculatorval += n + '' ;
      }
      if(n === 'C'){
        this.calculatorval = '';
      }
      if(n === '%') {
        this.calculatorval = this.calculatorval / 100 + '' ;
      }
      if(['/','*','-','+'].includes(n)){
        this.operator = n;
        this.prevCalcul = this.calculatorval;
        this.calculatorval = '';
      }
      if(n === '='){
        this.calculatorval = eval(
          this.prevCalcul + this.operator + this.calculatorval
        );
        this.prevCalcul = '';
        this.operator = null;
      }
    }
  }
  }

</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #963636;
}
</style>
<style scoped>
  .bg-vue-dark {
    background: #31475e;
  }
  .hover-class:hover {
    cursor: pointer;
    background: #3D5875;
  }
  .bg-vue-green {
    background: #963636;
  }
</style>