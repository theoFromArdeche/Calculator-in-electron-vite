<script setup lang="js">
//const ipcHandle = () => window.electron.ipcRenderer.send('ping')


var old_result = 0
var last_op = '+'

function numberOnClick(event) {
  const result = document.getElementById('result')
  if (result.innerText=='0') {
    result.innerText = event.target.innerText
  } else result.innerText += event.target.innerText
}

function acOnClick() {
  const result = document.getElementById('result')
  result.innerText = '0'
  old_result = 0
}

function operatorOnClick(event) {
  const operator = event.target.innerText
  const result = document.getElementById('result')
  if (last_op == '+') {
    old_result += parseInt(result.innerText)
  } else if (last_op == '-') {
    old_result -= parseInt(result.innerText)
  } else if (last_op == '/') {
    old_result /= parseInt(result.innerText)
  } else if (last_op == '*') {
    old_result *= parseInt(result.innerText)
  }
  if (operator == '=') {
    last_op = '+'
    result.innerText = Math.floor(old_result * 100) / 100
    old_result = 0
  } else {
    last_op = operator
    result.innerText = '0'
  }
  
}
</script>

<template>
  <div id="result_wrapper">
    <div id="result_div">
      <p id="result">0</p>
    </div>
  </div>
  <div id="buttons_wrapper">
    <button @click="acOnClick">ac</button>
    <button>+-</button>
    <button>%</button>
    <button @click="operatorOnClick">/</button>
    <button class="number" @click="numberOnClick">7</button>
    <button class="number" @click="numberOnClick">8</button>
    <button class="number" @click="numberOnClick">9</button>
    <button @click="operatorOnClick">*</button>
    <button class="number" @click="numberOnClick">4</button>
    <button class="number" @click="numberOnClick">5</button>
    <button class="number" @click="numberOnClick">6</button>
    <button @click="operatorOnClick">-</button>
    <button class="number" @click="numberOnClick">1</button>
    <button class="number" @click="numberOnClick">2</button>
    <button class="number" @click="numberOnClick">3</button>
    <button @click="operatorOnClick">+</button>
    <button id="button_0" class="number" @click="numberOnClick">0</button>
    <button>,</button>
    <button @click="operatorOnClick">=</button>
  </div>
</template>
