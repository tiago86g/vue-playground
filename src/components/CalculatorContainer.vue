<template>
  <div class="calculatorContainer">
    <div class="container">
      <div class="result truncate">
        {{ calculatorValue || 0}}
      </div>
      <div class="calculatorButtons">
        <div class="buttonItem" v-for="n in calculatorElements" :key='n'
        :class="{'symbols':['C', '*', '/', '-','+','%','=',].includes(n)}"
        @click="action(n)"
        >
          {{n}}
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="js">
export default {
  name: 'CalculatorContainer',
  props: {
    msg: String,
  },

  data() {
    return {
      calculatorValue: '',
      calculatorElements: ['C', '%', '/', '*', 7, 8, 9, '-', 4, 5, 6, '+', 1, 2, 3, '=', 0, '.'],
      operator: null,
      previousCalculatorValue: '',
    }
  },

  methods: {
    action(n) {
      if (!Number.isNaN(n) || n === '.') {
        this.calculatorValue += n.toString()
      }
      if (n === 'C') {
        this.calculatorValue = ''
      }
      if (n === '%') {
        this.calculatorValue = `${this.calculatorValue.slice(0, -1) / 100}`
      }
      if (['*', '/', '-', '+'].includes(n)) {
        this.operator = n
        this.previousCalculatorValue = this.calculatorValue
        // this.calculatorValue = '';
      }
      if (n === '=') {
        // eslint-disable-next-line no-eval
        this.calculatorValue = eval(
          this.calculatorValue.slice(0, -1),
          // this.previousCalculatorValue.slice(0, -1)
          // + this.operator
          // + this.calculatorValue.slice(0, -1),
        )
        this.previousCalculatorValue = ''
        this.operator = null
      }
    },
  },

}
</script>

<style scoped lang="scss">
.calculatorContainer{
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  background: rgb(255, 199, 136);
}
.container{
  display: flex;
  flex-direction: column;
  background: rgb(40, 39, 78);
  width: 25rem;
  max-width: 80vw;
  }
.result{
  font-weight: 700;
  font-size: 2.5rem;
  text-align: right;
  margin: 0.5rem 0.5rem 0;
  padding: 1rem;
  background: rgb(211, 212, 253);
}
.truncate {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
.calculatorButtons{
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 0.5rem;
  color: white;
  margin: 0.5rem;
  background: rgb(40, 39, 78);
}

.buttonItem{
  display: flex;
  justify-content: center;
  align-items: center;
  background: rgb(96, 97, 163);
  height: 5rem;
  font-size: 2rem;

  &:hover{
    background: rgb(149, 151, 243);
    cursor: pointer;
  }
}

.symbols{
  background: #eb6b39;
}
</style>

  // background: rgb(226, 226, 233);
  // border: rgb(40, 39, 78) solid 2rem;
  // background: rgb(96, 97, 163);
