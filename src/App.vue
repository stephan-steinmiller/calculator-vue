<template>
<div class="container">
  <div class="calculator">
    <div class="input-container">
      <div class="calculation">{{firstNumber +" "+ operator + " " + secondNumber}}</div>
      <div v-if="secondNumber=== '' ? '' : ' = ' " class="result">{{result}}</div>
    </div>
    <div class="calc-grid">
      <button class="btn calc-btn" @click="onAC">AC</button>
      <button class="btn calc-btn" @click="onNegate">-()</button>
      <button class="btn calc-btn" @click="onPercent">%</button>
      <button class="btn calc-btn" @click="onDivide">/</button>
      <button class="btn calc-btn" @click="onNumber($event.target.textContent)">7</button>
      <button class="btn calc-btn" @click="onNumber($event.target.textContent)">8</button>
      <button class="btn calc-btn" @click="onNumber($event.target.textContent)">9</button>
      <button class="btn calc-btn" @click="onMultiply">*</button>
      <button class="btn calc-btn" @click="onNumber($event.target.textContent)">4</button>
      <button class="btn calc-btn" @click="onNumber($event.target.textContent)">5</button>
      <button class="btn calc-btn" @click="onNumber($event.target.textContent)">6</button>
      <button class="btn calc-btn" @click="onSubtract">-</button>
      <button class="btn calc-btn" @click="onNumber($event.target.textContent)">1</button>
      <button class="btn calc-btn" @click="onNumber($event.target.textContent)">2</button>
      <button class="btn calc-btn" @click="onNumber($event.target.textContent)">3</button>
      <button class="btn calc-btn" @click="onAdd">+</button>
      <button class="btn calc-btn btn-zero" @click="onNumber($event.target.textContent)">0</button>
      <button class="btn calc-btn" @click="onDot">.</button>
      <button class="btn calc-btn orange" @click="onEqual">=</button>
    </div>
  </div>
</div></template>

<script>

const OPERATORS = {
  ADD: '+',
  MULTIPLY: '*',
  DIVIDE: '/',
  SUBTRACT: '-',
}

export default {
  name: 'App',
  components: {
  },
  data() {
    return {
      titleName: "Task Tracker",
      foreName: 'Stephan',
      surName: 'Steinmiller',
      counter: 0,
      firstNumber: '0',
      secondNumber: '',
      operator: '',
      intermediateResult: 0,
      number: 0,
    }
  },
  mounted() {
    console.log(this.titleName + " before change")
    this.titleName = "Super Task Tracker"
    console.log(this.titleName + " after change")
  },
  computed: {
    fullName() {
      return this.foreName + ' ' + this.surName
    },
    result() {
      let val = '';
      switch (this.operator) {
        case OPERATORS.ADD:
          val = +this.firstNumber + (+this.secondNumber)
          break;
        case OPERATORS.MULTIPLY:
          val = +this.firstNumber * (+this.secondNumber)
          break;
        case OPERATORS.DIVIDE:
          val = +this.firstNumber / (+this.secondNumber)
          break;
        case OPERATORS.SUBTRACT:
          val = +this.firstNumber - (+this.secondNumber)
          break;
      }
      return val
    }
  },
  methods: {
    onForeNameChange(){
      console.log('test');
    }, 
    subtract() {
      this.counter--
    },
    add() {
      this.counter++
    },
    myFunction() {
      console.log("my function was called")
    },
    onAdd() {
      if (this.result !== '' && this.secondNumber !== '0') {
        this.firstNumber = this.result
      }
      this.operator = OPERATORS.ADD
      this.secondNumber = '0'
    },
    onMultiply() {
      if (this.result !== '' && this.secondNumber !== '0') {
        this.firstNumber = this.result
      }
      this.operator = OPERATORS.MULTIPLY
      this.secondNumber = '0'
    },
    onDivide() {
      if (this.result !== '' && this.secondNumber !== '0') {
        this.firstNumber = this.result
      }
      this.operator = OPERATORS.DIVIDE
      this.secondNumber = '0'
    },
    onSubtract() {
      if (this.result !== '' && this.secondNumber !== '0') {
        this.firstNumber = this.result
      }
      this.operator = OPERATORS.SUBTRACT
      this.secondNumber = '0'
    },
    onNumber(stringValue) {
      if(this.operator === '') {
        if (this.firstNumber === '0') {
          this.firstNumber = ''
        }
        this.firstNumber += stringValue
        console.log(this.firstNumber);
      } else if(this.operator !== '') {
        if (this.secondNumber === '0') {
          this.secondNumber = ''
        }
        this.secondNumber += stringValue
      }
    },
    onAC() {
      this.firstNumber = '0'
      this.secondNumber = ''
      this.operator= ''
    },
    onHeaderTitleChanged(payload) {
      console.log('the new title is: ' + payload.title + ' and version is: ' + payload.version);
    }
  }
}
</script>

<style>
@media (orientation: landscape) {
  html {
    font-size: 0.5625vh;
  }
}

@media (orientation: portrait) {
  html {
    font-size: 0.5625vh;
  }
}
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
}
.container {
  display: flex;
  justify-content: center;
}
.calculator {
  display: flex;
  flex-direction: column;

  justify-content: flex-end;
  width: 100rem;
  overflow: auto;
  height: 100vh;
  padding: 2rem;
}
.btn {
  height: 18rem;
  min-width: 18rem;
  display: inline-block;
  background: #333333;
  color: #fff;
  border: none;
  border-radius: 999999px;
  cursor: pointer;
  text-decoration: none;
  font-size: 8rem;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
.calc-grid{
  flex-basis:98rem;
  max-width: 100rem;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-gap: 2rem;
}

.input-container{
  max-width: 100rem;
}
.calculation {
  font-size: 12rem;
  max-width: 100rem;
}
.result {
  font-size: 8rem;
  text-align: right;
}
.btn-zero{
  grid-area: 5 / 1 / 6 / 3;
}
.btn.orange {
  background-color: #fe9e0a;
}
.btn.grey {
  background-color:#a5a5a5;
}
</style>
