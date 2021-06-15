<template>
  <div class="calculator">
     <div class="display">{{current || '0'}}</div>
    <div @click="clear" class="btn">C</div>
    <div @click="sign" class="btn">+/-</div>
    <div @click="percent" class="btn">%</div>
    <div @click="divide" class="btn operator">÷</div>
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="times" class="btn operator">x</div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div @click="minus" class="btn operator">-</div>
    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div @click="add" class="btn operator">+</div>
    <div @click="append('0')" class="btn zero">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn operator equal">=</div>
    <div @click="sqrt" class="btn operator">sqrt</div>
    <div @click="exp" class="btn operator">e^</div>
    <div @click="pow" class="btn operator">pow</div>
    <div @click="log2" class="btn operator">log2</div>
    <div @click="sin" class="btn operator">sin</div>
    <div @click="cos" class="btn operator">cos</div>
    <div @click="tan" class="btn operator">tan</div>
    <div @click="log10" class="btn operator">log10</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      current: '',
      operator: null,
      operatorClicked: false,
    }
  },
  methods: {
    clear() {
      this.current = '';
    },
    sign() {
      this.current = this.current.charAt(0) === '-' ? 
        this.current.slice(1) : `-${this.current}`;
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
    append(number) {
      if (this.operatorClicked) {
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    dot() {
      if (this.current.indexOf('.') === -1) {
        this.append('.');
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    times() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    minus() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    add() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equal() {
      this.current = `${this.operator(
        parseFloat(this.current), 
        parseFloat(this.previous)
      )}`;
      this.previous = null;
    },
    sqrt() {
      this.operator = (a) => Math.sqrt(a);
      this.setPrevious();
    },
    exp() {
      this.operator = (a) => Math.exp(a);
      this.setPrevious();
    },
    pow() {
      this.operator = (a, b) => Math.pow(a,b);
      this.setPrevious();
    },
    log2() {
      this.operator = (a) => Math.log2(a);
      this.setPrevious();
    },
    sin() {
      this.operator = (a) => Math.sin(a);
      this.setPrevious();
    },
    cos() {
      this.operator = (a) => Math.cos(a);
      this.setPrevious();
    },
    tan() {
      this.operator = (a) => Math.tan(a);
      this.setPrevious();
    },
    log10() {
      this.operator = (a) => Math.log10(a);
      this.setPrevious();
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
* { 
    margin: 2px;
    padding: 0px;
    background-color: yellow;
    box-sizing:border-box;
}

.calculator{
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4,1fr);
  grid-auto-rows: minmax(50px,auto);
  border: 4px solid rgb(153, 153, 153);
}
.display{
  grid-column: 1/5;
  background-color: chartreuse;
  color: white;
  border: 2px solid rgb(153, 153, 153);
}
.zero {
  grid-column: 1 / 3;
}

.btn {
  background-color: #F2F2F2;
  border: 2px solid rgb(153, 153, 153);
}
.operator {
  background-color: rgb(0, 153, 255);
  color: white;
}
.equal {
  background-color: rgb(255, 72, 0);
  color: whitesmoke;
}
</style>
