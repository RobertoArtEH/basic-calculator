<template lang="pug">
  .cal
    .cal-box
      h2 {{ result }}
      p {{ operation }}
    .keypad
      .numbers
        button(@click="append('7')") 7
        button(@click="append('8')") 8
        button(@click="append('9')") 9

        button(@click="append('4')") 4
        button(@click="append('5')") 5
        button(@click="append('6')") 6

        button(@click="append('1')") 1
        button(@click="append('2')") 2
        button(@click="append('3')") 3

        button(@click="append('0')") 0
        button(@click="dot") .
      .operators
        span
          button(@click="handleOperator('/')") /
          button(@click="clear") C
        span
          button(@click="handleOperator('*')") *
        span
          button(@click="handleOperator('-')") -
        span
          button(@click="handleOperator('+')") +
          button(@click="equal") =
</template>

<script>
export default {
  data () {
    return {
      result: 0,
      current: '',
      log: '',
      operationClicked: false
    }
  },
  computed: {
    operation () {
      return `${this.log}${this.current}`
    }
  },
  methods: {
    append (number) {
      if (this.operationClicked) {
        this.current = ''
        this.operationClicked = false
      }

      this.current = `${this.current}${number}`
    },
    handleOperator (operator) {
      if (!this.operationClicked) {
        this.log += `${this.current} ${operator} `
        this.current = ''
        this.operationClicked = true
      }
    },
    dot () {
      if (this.current.indexOf('.') === -1) {
        this.append('.')
      }
    },
    equal () {
      if (!this.operationClicked) {
        /* eslint no-eval: 0 */
        this.result = eval(this.log + this.current)
      }
    },
    clear () {
      this.operationClicked = false
      this.current = ''
      this.result = 0
      this.log = ''
    }
  }
}
</script>

<style lang="scss">
  .cal {
    overflow: hidden;
    width: 20em;

    &-box {
      border: 1px solid gray;
      border-radius: 5px;
      text-align: right;
      margin: 1em auto;
      padding: 0 10px;
      height: 100px;
      width: 100%;
    }

    button {
      height: 3em;
    }
  }

  .keypad {
    display: grid;
    grid-template-columns: 2fr 1fr;
  }

  .numbers {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
  }

  .operators {
    display: grid;
    grid-template-columns: 2fr;

    button {
      width: 50%;
    }
  }
</style>
