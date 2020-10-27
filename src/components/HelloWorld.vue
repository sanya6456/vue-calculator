<template>
<div class="container">
    <div class="calculator">
      <div class="calculator-container">
        <div class="result">
          <div class="show-result">{{state.current||0}}</div>
        </div>
        <div class="row-one">
          <div class="seven" @click="append('7')">{{state.seven}}</div>
          <div class="eight" @click="append('8')">{{state.eight}}</div>
          <div class="nine" @click="append('9')">{{state.nine}}</div>
          <div class="clear" @click="clear">C</div>
        </div>
      <div class="row-two">
        <div class="four" @click="append('4')">{{state.four}}</div>
        <div class="five" @click="append('5')">{{state.five}}</div>
        <div class="six" @click="append('6')">{{state.six}}</div>
        <div class="multiplication" @click="multiplication">x</div>
      </div>
      <div class="row-three">
        <div class="one" @click="append('1')">{{state.one}}</div>
        <div class="two" @click="append('2')">{{state.two}}</div>
        <div class="three" @click="append('3')">{{state.three}}</div>
        <div class="divide" @click="divide">/</div>
      </div>
      <div class="row-four">
        <div class="zero" @click="append('0')">0</div>
        <div class="minus" @click="minus">-</div>
        <div class="plus" @click="plus">+</div>
        <div class="equal" @click="equal">=</div>
      </div>
      </div>
  </div>
</div>
</template>

<script>
import {reactive} from 'vue';
export default {
  name: 'HelloWorld',

  setup(){
    const state=reactive({
      one:1,
      two:2,
      three:3,
      four:4,
      five:5,
      six:6,
      seven:7,
      eight:8,
      nine:9,

      previous:null,
      current:'',
      operator:null,
      operatorClicked:false
    })
    // C
    function clear(){
      state.current='';
    }
    //append numbers after the last
    function append(number){
      if(state.operatorClicked){
        state.current='';
        state.operatorClicked=false
      }
      state.current+=number;
    }
    //take current to previous
    function setPrevious(){
      state.previous=state.current;
      state.operatorClicked=true
    }

    // + - / *
    function multiplication(){
      state.operator=(a,b)=>a*b;
      setPrevious()
    }
    function plus(){
      state.operator=(a,b)=>a+b;
      setPrevious()
    }
    function minus(){
      state.operator=(a,b)=>a-b;
      setPrevious()
    }
    function divide(){
      state.operator=(a,b)=>b/a;
      setPrevious()

    }
    // equal and maximize decimals
    function equal(){
      state.current=state.operator(parseFloat(state.current),parseFloat(state.previous));
      
    }

    return{
      state,
      clear,
      multiplication,
      append,
      plus,
      minus,
      divide,
      equal,
      setPrevious
    }
    
    
  }

}
</script>


<style scoped lang="scss">
.container{
  min-height: 100vh;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;

  color: white;
  .calculator{
    width: 400px;
    height: 600px;
    margin: auto;

    background-color: #242323;
    border-radius: 32px;
    box-shadow: 5px 8px 5px rgb(0, 0, 0);
    .calculator-container{
      width: 100%;
      height: 100%;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      .row-one, .row-two, .row-three, .row-four{
        display: flex;
        justify-content: space-around;
        align-items: center;
        width: 90%;
        height: 100%;
        div{
          padding: 1.8rem 2rem;
          border-radius: 16px;
          border: 1px solid rgb(184, 184, 184);
          font-size: 1.8rem;

          cursor: pointer;
          &:hover{
            background-color: #fff;
            color: #000;
          }
        }
        .equal, .minus, .plus, .divide, .multiplication{
          background-color: rgb(90, 21, 21);
        }
      }
      .result{
        height: 30%;
        width: 100%;
        display: flex;
        flex-direction: column;
        justify-content: center;
        .show-result{
          width: 95%;
          padding: 1.8rem;
          border-radius: 22px;
          margin: .5rem auto;
          color: #000;
          font-size: 2rem;
          background-color: #fff;
          text-align: center;
        }
      }
    }
  }
}

</style>
