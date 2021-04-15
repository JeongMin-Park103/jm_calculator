<template>
  <div class="calculator">
    <div class="display">{{current || '0'}}</div>
    <div @click="clear" class="btn1">C</div>
    <div @click="sign" class="btn1">+/-</div>
    <div @click="del" class="btn1">DEL</div>
    <div @click="divide" class="btn operator">/</div>
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="multi" class="btn operator">x</div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div @click="minus" class="btn operator">-</div>
    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div @click="plus" class="btn operator">+</div>
    <div @click="append('0')" class="btn zero">0</div>
    <div @click="dot()" class="btn">.</div>
    <div @click="equal()" class="btn operator">=</div>
  </div>
</template>

<script>
export default{
  data(){
    return{
      previous: null,
      current: '',
      operator: null,
      operatorClicked: false,

    }
  },
  methods:{
    clear(){
      this.current = '';
    },
    sign(){
      this.current = this.current.charAt(0) === '-' ? 
        this.current.slice(1) : `-${this.current}`;
    },

    del(){     
        this.current = this.current.substring(0, this.current.length -1);
          if (this.current === ''){
                this.previous == 0;
              }
          
          else{
              this.previous = this.current;
            }

          if (this.previous == '-'){
            this.current = '';
          }
    },

    append(number){
      if (this.operatorClicked == true){
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },

    dot(){
      if (this.current.indexOf('.') === -1){
        this.append('.');
      }
    },

    setPrevious(){
      this.previous = this.current;
      this.operatorClicked = true;
    },

    divide(){
      this.operator = (a, b) => b / a;
      this.setPrevious();
    },

    multi(){
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },

    minus(){
      this.operator = (a, b) => - a + b;
      this.setPrevious();
    },

    plus(){
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },

    equal(){
     this.current = `${this.operator(
        parseFloat(this.current),
        parseFloat(this.previous)
      )}`;
     this.previous = null;
    }

  }
}  
</script>

<style>
.calculator{
  width: 400px;
  margin: 0 auto;
  font-size: 48px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}

.display{
  grid-column: 1 / 5;
  background-color: black;
  color: white;
}

.zero{
  grid-column: 1 / 3;
  background-color: gray;
  border: 1px solid #333;
  color: white;
}

.btn1{
  background-color: rgb(164, 163, 163);
  border: 1px solid #333;
  color: white;

}

.btn{
  background-color: rgb(103, 100, 100);
  border: 1px solid #333;
  color: white;

}

.operator{
  background-color: rgba(187, 75, 10, 0.898);
  color: white;
}

</style>