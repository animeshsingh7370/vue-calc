<template>
 <div class="calculator">
      <div class="profile">
        <img class="menu-icon" src="@/assets/menu.png"  alt="">
        <h3>Calculator</h3>
        <img class="profile-img" src="@/assets/dalli-mask.png"  alt="">
      </div>
      <textarea  class="exp-box"  v-model="expValue" @input="validateInput" ></textarea>
      <div class="button-box">
          <button class="ac" @click="reset()">AC</button>
          <button class="delete" @click="deleteLast()" >DEL</button>
          <button class="modulus" @click="appendValue('%')">%</button>
          <button class="divide" @click="appendValue('/')">/</button>
          <button class="square_rt" @click="appendValue('3.14')">&Pi;</button>
          <button class="seven" @click="appendValue('7')">7</button>
          <button class="eight" @click="appendValue('8')">8</button>
          <button class="nine" @click="appendValue('9')">9</button>
          <button class="multiply" @click="appendValue('*')">*</button>
          <button class="open_bra" @click="appendValue('(')">(</button>
          <button class="four" @click="appendValue('4')">4</button>
          <button class="five" @click="appendValue('5')">5</button>
          <button class="six" @click="appendValue('6')">6</button>
          <button class="minus" @click="appendValue('-')">-</button>
          <button class="close_bra" @click="appendValue(')')">)</button>
          <button class="one" @click="appendValue('1')">1</button>
          <button class="two" @click="appendValue('2')">2</button>
          <button class="three" @click="appendValue('3')">3</button>
          <button class="plus" @click="appendValue('+')">+</button>
          <button class="equal" @click="calculate()">=</button>
          <button class="point" @click="appendValue('.')">.</button>
          <button class="square" @click="appendValue('^')">^</button>
          <button class="zero" @click="appendValue(0)">0</button>
          
        

      </div>
 </div>
</template>

<script>


export default {
  data() {
    return {
      expValue: '',
      calcExp: ''
      
    };
  },
  methods: {
    validateInput() {
      // Allow only numbers and specific characters
      this.expValue = this.expValue.replace(/[^0-9+\-*().]/g, '');
    },
    appendValue(value){
      // console.log("ac");
      if (this.expValue == 'Error'){
        this.expValue = '';
        this.expValue += value;
      }else{
        this.expValue += value;
      }
      
    },
    reset(){
      this.expValue = '';
    },
    deleteLast(){
      if (this.expValue == 'Error'){
        this.expValue = '';
      }this.expValue = this.expValue.slice(0, -1);
      
    },
    calculate(){
      if (this.expValue == 'Error'){
        this.expValue = '';
      }else{
        
        try {
        this.calcExp = this.expValue.replace('^', '**')
        this.calcExp = this.calcExp.replace('&Pi;', '3.14')
        
        this.expValue = String(eval(this.calcExp));
      } catch (error) {
        console.error(error);
        this.expValue = 'Error';
      }
      }

    }
  }
}
</script>

