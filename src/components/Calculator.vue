<template>
<div>
  <h1>{{ title }}</h1>
  <div class="elements">
    <div class= "result btn">{{result || 0}}</div>
    <div @click = "clear" class='btn'>C</div>
    <div @click = "operator" class='btn'>+/-</div>
    <div @click = "percent" class='btn'>%</div>
    <div @click = "divide" class='sign btn'>/</div>
    <div @click = "attach('7')" class='btn'>7</div>
    <div @click = "attach('8')" class='btn'>8</div>
    <div @click = "attach('9')" class='btn'>9</div>
    <div @click = "times" class='sign btn'>x</div>
    <div @click = "attach('4')" class='btn'>4</div>
    <div @click = "attach('5')" class='btn'>5</div>
    <div @click = "attach('6')" class='btn'>6</div>
    <div @click = "minus" class='sign btn'>-</div>
    <div @click = "attach('1')" class='btn'>1</div>
    <div @click = "attach('2')" class='btn'>2</div>
    <div @click = "attach('3')" class='btn'>3</div>
    <div @click = "plus" class='sign btn'>+</div>
    <div @click = "attach('0')" class ='zero btn'>0</div>
    <div @click = "dot" class='btn'>.</div>
    <div @click = "equal" class='sign btn'>=</div>
  </div>
  </div>
</template>

<script>
export default {
 data() {
   return {
     title: 'Simple Calculator',
     previous: null,
     result: '',
     sign: null,
     signClicked:false
   }
 },

 methods: {
   clear() {
     this.result = ''
   },
   operator(){
     this.result = this.result.charAt(0) === '-' ?
       this.result.slice(1) : `-${this.result}`;
   },
   percent() {
     this.result = `${parseFloat(this.result / 100)}`
   },
   attach(number){
     if(this.sign){
       this.result = '';
       this.signClicked= ''
     }
     this.result =`${this.result}${number}`
   },
   dot(){
     if(this.result.indexOf('.') === -1){
       this.attach('.')
     }
   },
   plus(){
     this.sign = (a, b) => a + b;
     this.previous = this.result;
     this.signClicked = true
   },
   divide(){
     this.sign = (a, b) => a / b;
     this.previous = this.result;
     this.signClicked = true
   },
   times(){
     this.sign = (a, b) => a * b;
     this.previous = this.result;
     this.signClicked = true
   },
   minus(){
     this.sign = (a, b) => a - b;
     this.previous = this.result;
     this.signClicked = true
   },
   equal(){
     this.result = `${this.sign(parseFloat(this.result),parseFloat(this.previous))}`;
     this.previous = null;
   }
 }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1{
  text-align: center;
}
.elements{
  align-content: center;
  background-color: #ddd;
  box-shadow: 7px 7px 4px #000;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  margin: 0 auto;
  width: 20%;
}
.btn{
  border: 1px solid #333;
}
.result{
  grid-column: 1/5;
  background-color:#000;
  color: #fff;
  text-align: right;
}
.zero{
  grid-column: 1/3;
}
.sign{
  background-color: grey; 
}
</style>
