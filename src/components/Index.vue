<template>
  <div class="wrapper">
    <h1>Vue Calculator</h1>
    <div class="inner-wrapper">
      <div class="inner">
         <h1>{{currentNumber}}</h1>
          <div v-if="selectedOperation" class="p">
            <p>{{prevNumber}} {{selectedOperation}} {{currentNumber}}</p>
          </div>
      </div>
     
      
      <div class="keyboard">
        <button @click="pressed('1')">1</button>
        <button @click="pressed('2')">2</button>
        <button @click="pressed('3')">3</button>
        <button @click="pressed('+')">+</button>
        <button @click="pressed('4')">4</button>
        <button @click="pressed('5')">5</button>
        <button @click="pressed('6')">6</button>
        <button @click="pressed('-')">-</button>
        <button @click="pressed('7')">7</button>
        <button @click="pressed('8')">8</button>
        <button @click="pressed('9')">9</button>
        <button @click="pressed('*')">x</button>
        <button @click="pressed('c')">C</button>
        <button @click="pressed('0')">0</button>
        <button @click="pressed('=')">=</button>
        <button @click="pressed('/')">/</button>
      </div>
    </div>
  </div>
</template>

<script>
import {onMounted, ref} from 'vue'
export default {
  name: 'Index',
  setup(){

    const operation =['+','-','*','/']
    const number = ['1','2','3','4','5','6','7','8','9','0']
    const currentNumber = ref('')
    const prevNumber = ref('')
    const selectedOperation = ref('')

    function pressed(value){
      if(value == '=') calculate()
      else if (value == 'c') clear()
      else if (operation.includes(value)) applyOperation(value)
      else if(number.includes(value)) appendNumber(value)


    }

    function appendNumber(value){
      currentNumber.value = currentNumber.value + value
    }

    function clear(){
      currentNumber.value = ''
      prevNumber.value = ''
      selectedOperation.value = ''
    }

    function calculate(){
      if(selectedOperation.value == '+') sum()
      if(selectedOperation.value == '-') distract()
      if(selectedOperation.value == '*') multiply()
      if(selectedOperation.value == '/') divide()

      prevNumber.value = ''
      selectedOperation.value=''
      
    }

    function applyOperation(value){
      calculate()
      prevNumber.value = currentNumber.value
      currentNumber.value = ''
      selectedOperation.value = value 
     
    }

    function sum(){
      currentNumber.value = +prevNumber.value + +currentNumber.value
    }

    function distract(){
      currentNumber.value = prevNumber.value - currentNumber.value
    }

    function multiply(){
      currentNumber.value = prevNumber.value * currentNumber.value
    }

    function divide(){
      currentNumber.value = prevNumber.value / currentNumber.value
    }

    onMounted(() =>{
      window.addEventListener('keydown', e=>{
        console.log(e.key);
        pressed(e.key)
      })
    })





    return{
      currentNumber, pressed, prevNumber, selectedOperation
    }
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.wrapper{
 
  width: 700px;
  margin: auto;
  text-align: center;
}

.inner-wrapper{
  
  width: 300px;
  margin: 70px auto 0  auto;
  padding: 10px;
  box-shadow: 3px 3px #f3f3f3;
  border: 1px solid #f3f3f3;
  
}

.inner-wrapper .inner{
  border: 1px solid #f3f3f3;
}

.inner-wrapper h1{
  text-align: right;
  overflow: hidden;
  direction: rtl;
  height: 30px;
 
}

.p{
  height: 20px;
  text-align: left;
}


button{
  padding: 15px 15px;
  font-size: 25px;
  margin: 5px;

}

.keyboard{
   display: grid;
  grid-template-columns: repeat(4, 1fr);
}
</style>
