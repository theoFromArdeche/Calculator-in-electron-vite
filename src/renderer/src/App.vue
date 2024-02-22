<script setup lang="js">
//const ipcHandle = () => window.electron.ipcRenderer.send('ping')

var old_result = 0
var last_op = '+'

function numberOnClick(event) {
  const result = document.getElementById('result')
  if (result.innerText == '0') {
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
  if (operator == '+-') {
    if (result.innerText == '0') return
    if (result.innerText[0] == '-') {
      result.innerText = result.innerText.slice(1)
    } else {
      result.innerText = '-' + result.innerText
    }
    return
  } else if (operator == ',') {
    result.innerText += '.'
    return
  }

  if (last_op == '+') {
    old_result += parseFloat(result.innerText)
  } else if (last_op == '-') {
    old_result -= parseFloat(result.innerText)
  } else if (last_op == '/') {
    old_result /= parseFloat(result.innerText)
  } else if (last_op == '*') {
    old_result *= parseFloat(result.innerText)
  } else if (last_op == 'MOD') {
    old_result %= parseFloat(result.innerText)
  }
  if (operator == '=') {
    last_op = '+'
    result.innerText = Math.floor(old_result * 1000) / 1000
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
    <button @click="operatorOnClick">+-</button>
    <button id="button_MOD" @click="operatorOnClick">MOD</button>
    <button @click="operatorOnClick">/</button>
    <button @click="numberOnClick">7</button>
    <button @click="numberOnClick">8</button>
    <button @click="numberOnClick">9</button>
    <button @click="operatorOnClick">*</button>
    <button @click="numberOnClick">4</button>
    <button @click="numberOnClick">5</button>
    <button @click="numberOnClick">6</button>
    <button @click="operatorOnClick">-</button>
    <button @click="numberOnClick">1</button>
    <button @click="numberOnClick">2</button>
    <button @click="numberOnClick">3</button>
    <button @click="operatorOnClick">+</button>
    <button id="button_0" @click="numberOnClick">0</button>
    <button @click="operatorOnClick">,</button>
    <button @click="operatorOnClick">=</button>
  </div>
</template>
