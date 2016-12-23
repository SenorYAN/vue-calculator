<template>
  <div id="calculator">
    <result v-bind:title="answer" />
    <div id="panel-wrapper">
      <div id="number-panel">
        <numberButton  v-for="number in numbers" :value="number" v-on:onSetNumber="setNumber"/>
      </div>
      <div id="calculate-panel">
        <calculateButton  v-for="func in calculateFuncs" :value="func" v-on:onCalculate="calculateFunc"/>
      </div>
      <div class="equal-button button" v-on:click="doCalculate">=</div>
    </div>
  </div>
</template>

<script>
import result from './components/result.vue';
import numberButton from './components/number-button.vue';
import calculateButton from './components/calculate-button.vue';
export default {
  name: 'calculator',
  data () {
    return {
      answer: 0,
      getAnswer: function(){return this.answer},
      setAnswer: function(answer){this.answer = answer},
      numbers: ['1','2','3','4','5','6','7','8','9','0','.','MC'],
      calculateFuncs: ['+','-','*','/'],
      arg:[0,0,''],//运算数组，[参数1、参数2、运算类型]
      IS_DOT: false//是否点击了小数点
    }
  },
  methods: {
    setNumber : function(n){
      if(n!='.'&&n!='MC'){
        console.log('typed: ' + n + ' current-answer: '+ this.answer + ' ISDOT is ' + this.IS_DOT);
        let _dotSum = this.answer.toString().split('.')[1];
        if(!this.IS_DOT){//整数->整数
          this.setAnswer((this.answer-0)*10+(n-0));
        }else if(_dotSum){//小数->小数
          this.setAnswer((this.answer-0)+Math.pow(10,(_dotSum.length+1)*(-1))*(n-0));
        }else{//整数->小数
          this.setAnswer((this.answer-0)+0.1*(n-0))
        }
      }else if(n=='.'){
        console.log('typed .');
        this.IS_DOT = true;
      }else{
        console.log('typed mc');
        this.setAnswer(0);
        this.IS_DOT = false;
        this.arg = [0,0,''];
      }
    },
    calculateFunc : function(fName){
      console.log(fName);
      this.arg[0] = this.answer;//把目前的answer放到第一个运算参数
      this.arg[2] = fName;
      this.setAnswer(0);
    },
    doCalculate: function() {
      console.log('typed =')
      let _sum = 0;
      switch(this.arg[2]){
        case '+':
          _sum = this.arg[0] + this.answer;
        break;
        case '-':
          _sum = this.arg[0] - this.answer;
        break;
        case '*':
          _sum = this.arg[0] * this.answer;
        break;
        case '/':
          _sum = this.arg[0] / this.answer;
        break;
        default:
          _sum = this.answer;
        break;
      }
      this.setAnswer(_sum);
      this.arg[2] = ''
    }
  },
  components: { result, numberButton, calculateButton }
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
}
html,body{
  width: 100%;
  height: 100%;
}
body{
  display: flex;
  justify-content: center;
  align-items: center;
}
#calculator{
  width: 370px;
  box-shadow: 0px 0px 20px 0px #333;
  border-radius: 4px;
  padding: 15px;
}
#panel-wrapper{
  display: flex;
  flex-wrap: wrap;
  padding-top: 20px;
}
#number-panel{
  display: flex;
  justify-content: flex-start;
  flex-wrap: wrap;
  width: 75%;
}
#calculate-panel{
  display: flex;
  justify-content: flex-start;
  flex-wrap: wrap;
  width: 25%;
}
.equal-button{
  margin-top: 10px;
  width: 100%;
  border: 1px solid #000;
  height: 60px;
  border-radius: 8px;
  font-size: 30px;
  line-height: 60px;
  text-align: center;
}
.button:hover{
  border-color: rgb(49, 163, 219);
  box-shadow:0 0 10px 0 rgba(49, 163, 219,0.3);
  color: rgb(49, 163, 219);
}
</style>
