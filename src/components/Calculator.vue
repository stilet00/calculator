<template>
  <div id="calc" class="calculator">
    <button class="display">{{current || 0.00}}</button>
    <button @click="clear">C</button>
    <button @click="module" class="operator">+/-</button>
    <button class="operator" @click="percent">%</button>
    <button class="operator" @click="operatorsClick('/')">/</button>
    <button @click="append('7')">7</button>
    <button @click="append('8')">8</button>
    <button @click="append('9')">9</button>
    <button class="operator" @click="operatorsClick('x')">x</button>
    <button @click="append('4')">4</button>
    <button @click="append('5')">5</button>
    <button @click="append('6')">6</button>
    <button class="operator" @click="operatorsClick('-')">-</button>
    <button @click="append('1')">1</button>
    <button @click="append('2')">2</button>
    <button @click="append('3')">3</button>
    <button class="operator" @click="operatorsClick('+')">+</button>
    <button class="zero" @click="append('0')">0</button>
    <button @click="append('.')">.</button>
    <button @click="equal" class="operator">=</button>
  </div>
</template>

<script>
  export default {
    name: 'Calculator',
    data() {
      return {
        current: '200',
        calculating: '',
        previous: '',
        operatorClicked: false,
        operator: ''
      }

    },
    methods: {
      clear() {
        this.current = ''
      },
      module() {
        if (Number(this.current) > 0) {
          let minus = this.current.split('');
          minus.unshift('-')
          this.current = minus.join('')
        } else if (Number(this.current) < 0){
          let plus = this.current.split('');
          plus.shift('-');
          this.current = plus.join('');
        }
      },
      percent() {
        this.current!='' ? this.current = `${parseFloat(this.current) / 100}` : this.current = ''
      },
      append(number) {
        if (number !== '.') {
          this.current = this.current + number;
        } else if (!this.current.includes('.')) {
          this.current = this.current + number;
        }

      },
      setPrevious() {
        this.previous = this.current;
        this.operatorClicked = true;
      },
      operatorsClick(operatorKind) {
        this.setPrevious();
        this.operator = operatorKind;
        this.current = ''

      },

      equal() {
        if (this.operatorClicked) {
          switch (this.operator) {
            case ('/'): {
              this.current = (Number(this.previous) / Number(this.current)).toString();
              this.operator = '';
              this.previous = '';
              this.operatorClicked = 'false';
              break;
            }
            case ('+'): {
              this.current = (Number(this.previous) + Number(this.current)).toString();
              this.operator = '';
              this.previous = '';
              this.operatorClicked = 'false';
              break;
            }
            case ('-'): {
              this.current = (Number(this.previous) - Number(this.current)).toString();
              this.operator = '';
              this.previous = '';
              this.operatorClicked = 'false';
              break;
            }
            case ('x'): {
              this.current = (Number(this.previous) * Number(this.current)).toString();
              this.operator = '';
              this.previous = '';
              this.operatorClicked = 'false';
              break;
            }
          }
        }

      }

    }

}


</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  button {
    background: #c4c3c3;
    transition: 1s;
  }
  button:focus {
    background: white;
  }
.calculator {
  width: 50%;
  margin: 0 auto;
  border-radius: 5px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}
.operator {
  background: darkorange;
}

  .display {
    padding-right: 20px;
    font-size: 25px;
    height: 100px;
    text-align: right;
    grid-column: 1 / 5;
    background: lightslategrey;
  }
  .zero {
    grid-column: 1 / 3
  }
</style>
