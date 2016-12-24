<template>
  <div class="result" >
    <h1><div :class="setFn">{{funcName}}</div>{{title}}</h1>
  </div>
</template>
<script>
  export default {
    props: ['title','funcName'],
    data(){
      return {
        fn : ''
      }
    },
    computed : {
      setFn: function(){
        switch(this.funcName){
          case '+':
            this.fn = 'add'
          break;
          case '-':
            this.fn = 'minus'
          break;
          case '*':
            this.fn = 'times'
          break;
          case '/':
            this.fn = 'divide'
          break;
          default:
            this.fn = ''
          break;
        }
        return this.fn;
      }
    }
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
    position: relative;
    margin: 0 20px;
    line-height: 60px;
    font-size: 26px;
  }
  .result h1>div{
    position: absolute;
    left: 0;
  }
  .result h1>div.add{
    color: rgba(230, 55, 92, 0.6);
  }
  .result h1>div.minus{
    color: rgba(129, 233, 179,0.6);
  }
  .result h1>div.times{
    color: rgba(233, 177, 51, 0.6)
  }
  .result h1>div.divide{
    color: rgba(188, 84, 244, 0.6);
  }
</style>
