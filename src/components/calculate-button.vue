<template>
  <div class="calculate-button button" v-on:click="handleClickFuncs">
    {{value}}
  </div>
</template>
<script>
  export default {
    props: ['value'],
    methods: {
      handleClickFuncs: function() {
        this.$emit('onCalculate',this.value)
      }
    }
  }
</script>
<style>
  .calculate-button{
    width: 70px;
    height: 70px;
    margin: 10px;
    border: 1px solid #000;
    border-radius: 50%;
    font-size: 30px;
    text-align: center;
    line-height: 70px;
    font-weight: bold;
    cursor: pointer;
  }
</style>
