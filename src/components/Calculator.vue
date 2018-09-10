<template>
  <div class="calculator">
    <div 
      class="comDisplay">{{ workSpace || '0' }}</div>
    
    <div 
      class="display">{{ current || '0' }}</div>
    
    <div 
      @click="clear" 
      class="btn">CE</div>
    
    <div 
      @click="del" 
      class="btn">C</div>
    
    <div 
      @click="percent" 
      class="btn">%</div>
    
    <div 
     @click="divide" 
      class="btn">/</div>
    
    <div 
      @click="append('7')" 
      class="btn-n">7</div>

    <div 
      @click="append('8')" 
      class="btn-n">8</div>

    <div 
      @click="append('9')" 
      class="btn-n">9</div>

    <div 
      @click="times" 
      class="btn">*</div>

    <div
       @click="append('4')" 
       class="btn-n">4</div>

    <div 
      @click="append('5')" 
      class="btn-n">5</div>
    
    <div 
      @click="append('6'), 
      logNum('6')" 
      class="btn-n">6</div>

    <div 
      @click="minus, 
      logNum('-')" 
      class="btn">-</div>

    <div 
      @click="append('1')" 
      class="btn-n">1</div>
    
    <div 
      @click="append('2')" 
      class="btn-n">2</div>  
    
    <div 
      @click="append('3')" 
      class="btn-n">3</div>
    
    <div 
      @click="plus" 
      class="btn">+</div>
    
    <div 
      @click="sign" 
      class="btn">+/-</div>
    
    <div 
      @click="append('0')" 
      class="btn-n">0</div>
    
    <div 
      @click="dot" 
      class="btn">.</div>
    
    <div 
      @click="equal" 
      class="btn">=</div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      previous: null,
      current: '',
      workSpace: '',
      operator: null,
      operatorClicked: false,
    }
  },
  methods: {
    clear () {
      this.current = '';
    },
    sign () {
     if (this.current.charAt(0) === '-') {
       this.current = this.current.substr(0);
     }else{
       this.current = '-' + this.current;
     }
    },
    del () {
      this.workSpace = 'Del' + this.current.charAt(-1);
      this.current = this.current.slice(0, -1);
    },
    percent () {
      this.workSpace = this.current + '/100';
      this.current = this.current / 100;
      
    },
    append(number) {            
      this.current = `${this.current}${number}`;
    },

    logNum(number) {
      this.workSpace = `${this.workSpace}${number}`;
    },


    dot() {
      if (this.current.indexOf('.') === -1) {
        this.append('.');
      }
    },

    compute() {
      this.previous = this.current;
      this.operatorClicked = true;
      this.clear();
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.compute()
    },
    plus() {
      this.operator = (a, b) => a + b;
      this.compute()
    },
    minus() {
      this.operator = (a, b) => a - b;
      this.compute()
    },
    times() {
      this.operator = (a, b) => a * b;
      this.compute()
    },
    equal() {
      this.current = `${this.operator(parseFloat(this.previous), parseFloat(this.current))}`;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator {
  margin: 0 auto;
  background-color: #e5e5e5;
  font-size: 32px;
  font-weight: bold;
  display: grid;
  max-height: 100%;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(70px, auto);
  grid-column-gap: 5px;
  grid-row-gap: 5px;
}
.comDisplay {
  font-size: 16px;
  color: #939393;
  text-align: right;
  grid-column: 1/5;
  padding: 15px;
}
.display {
  grid-column: 1/5;
  padding: 15px;
  text-align: right;
}
.btn {
  background-color: #eff1f4;
}
.btn-n {
  background-color: #fff;
}
.btn-n:hover {
  color: #fff;
  background-color: #939393;
}
.btn:hover {
  color: #fff;
  background-color: #1acc0a;
}

.btn, .btn-n {
  padding: 15px;
  text-align: center;
 

}

</style>
