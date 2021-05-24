<template lang="pug">
  .container
    h1 Calculator
    Calculator
</template>

<script>
import Calculator from '@/components/Calculator'

export default {
  name: 'Home',
  components: {
    Calculator
  }
}
</script>

<style lang="scss">
  .container {
    width: 100%;
    margin-left: auto;
    margin-right: auto;
    padding-left: 3rem;
    padding-right: 3rem;
  }
</style>
