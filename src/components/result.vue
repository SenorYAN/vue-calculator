<template>
  <div class="result" >
    <h1>{{title}}</h1>
  </div>
</template>
<script>
  export default {
    props: ['title']
  }
</script>
<style>
  .result{
    width: 100%;
    height: 58px;
    text-align: right;
    border: 1px solid #666;
    border-radius: 8px;
    box-shadow: 0 0 40px 0px rgba(0,0,0,0.3) inset
  }
  .result:hover{
    border-color: rgb(49, 163, 219);
    box-shadow: 0 0 10px 0px rgba(49, 163, 219,0.3)
  }
  .result h1{
    margin: 0 20px;
    line-height: 60px;
    font-size: 26px;
  }
</style>
