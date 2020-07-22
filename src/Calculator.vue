<template>
  <div class="calculator d-flex flex-column">
    <div class="d-flex flex-row">{{ display }}</div>
    <div class="d-flex flex-row">
      <button class="btn btn-light">AC</button>
      <button class="btn btn-light">%</button>
      <button class="btn btn-light" v-on:click="setMathFunction('divide')">
        /
      </button>
    </div>
    <div class="d-flex flex-row">
      <button class="btn btn-light" v-on:click="addValueIfAllowed('7')">
        7
      </button>
      <button class="btn btn-light" v-on:click="addValueIfAllowed('8')">
        8
      </button>
      <button class="btn btn-light" v-on:click="addValueIfAllowed('9')">
        9
      </button>
      <button class="btn btn-light" v-on:click="setMathFunction('multiply')">
        x
      </button>
    </div>
    <div class="d-flex flex-row">
      <button class="btn btn-light" v-on:click="addValueIfAllowed('4')">
        4
      </button>
      <button class="btn btn-light" v-on:click="addValueIfAllowed('5')">
        5
      </button>
      <button class="btn btn-light" v-on:click="addValueIfAllowed('6')">
        6
      </button>
      <button class="btn btn-light" v-on:click="setMathFunction('subtract')">
        -
      </button>
    </div>
    <div class="d-flex flex-row">
      <button class="btn btn-light" v-on:click="addValueIfAllowed('1')">
        1
      </button>
      <button class="btn btn-light" v-on:click="addValueIfAllowed('2')">
        2
      </button>
      <button class="btn btn-light" v-on:click="addValueIfAllowed('3')">
        3
      </button>
      <button class="btn btn-light" v-on:click="setMathFunction('add')">
        +
      </button>
    </div>
    <div class="d-flex flex-row">
      <button class="btn btn-light" v-on:click="addValueIfAllowed('0')">
        0
      </button>
      <button class="btn btn-light" v-on:click="addValueIfAllowed('.')">
        .
      </button>
      <button class="btn btn-light">=</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    periodUsed: false,
    functionSelected: '',
    total: 0,
    interactor: 'null',
    finalValueSet: false,
  },
  data() {
    return {
      mathFunction: '',
      display: '0',
    }
  },
  methods: {
    add() {
      return this.total + this.interactor
    },
    subtract() {
      return this.total - this.interactor
    },
    multiply() {
      return this.total * this.interactor
    },
    divide() {
      return this.total / this.interactor
    },
    remainder() {
      return this.total % this.interactor
    },
    setMathFunction(name) {
      this.mathFunction = name
    },
    addValueIfAllowed(string) {
      let value = parseFloat(string)
      // Check if maxCharacter count has been reached.
      if (this.display.length >= 8 && !this.periodUsed) {
        return
      }

      // Check if '.' has been used yet, if so, do nothing.
      if (
        (value === '.' && this.periodUsed) ||
        (value === parseFloat(this.display)) === 0
      ) {
        return
      }

      // Check if display is at initial display.
      if (this.display === '0' && value !== '.') {
        this.display = ''
      }

      this.display += value.toString()
    },
    runMathFunction() {
      return this[this.mathFunction]()
    },
  },
}
</script>
