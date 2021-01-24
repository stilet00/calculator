<template>
  <div id="calc" class="calculator">
    <button class="display">{{current || 0.00}}</button>
    <button @click="clear">C</button>
    <button @click="module" class="operator">+/-</button>
    <button class="operator" >%</button>
    <button class="operator">/</button>
    <button>7</button>
    <button>8</button>
    <button>9</button>
    <button class="operator">x</button>
    <button>4</button>
    <button>5</button>
    <button>6</button>
    <button class="operator">-</button>
    <button>1</button>
    <button>2</button>
    <button>3</button>
    <button class="operator">+</button>
    <button class="zero">0</button>
    <button >.</button>
    <button class="operator">=</button>
  </div>
</template>

<script>
  export default {
    name: 'Calculator',
    data() {
      return {
        current: '234'
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
      }
    }

}


</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  button {
    background: #eee
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
