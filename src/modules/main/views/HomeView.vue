<script setup lang="ts">
import { ref } from 'vue'
import { BtnNumber } from '../components'

const display = ref<string>('0')
const displayAction = ref<string>('')

const num1 = ref(0)
const num2 = ref(0)
const action = ref<string | null>(null)

const updateDisplay = (value: number | string) => {
  if (display.value === '0') display.value = ''
  display.value += value
}

const resetAll = () => {
  resetDisplay()
  resetNumbers()
  resetDisplayAction()
}

const resetDisplay = () => {
  display.value = '0'
}
const resetDisplayAction = () => {
  displayAction.value = ''
}

const resetNumbers = () => {
  num1.value = 0
  num2.value = 0
  action.value = null
}

const updateDisplayAction = () => {
  if (displayAction.value === '')
    displayAction.value = num1.value + ' ' + action.value
  else {
    displayAction.value += displayAction.value
  }
}

const sum = () => {
  action.value = '+'
  if (num1.value === 0) {
    num1.value = +display.value
    updateDisplayAction()
    resetDisplay()
  }
}

const calculate = () => {
  // num2.value = +display.value
  display.value = (num1.value + +display.value).toString()
  resetDisplayAction()
  //resetDisplay()
  resetNumbers()
}

const btn = [9, 8, 7, 6, 5, 4, 3, 2, 1]
</script>
<template>
  <v-container class="ma-0 pa-0">
    <v-card
      class="d-flex flex-column justify-center align-end pr-2"
      height="100"
      variant="tonal"
    >
      <div class="text-">{{ displayAction }}</div>
      <div class="text-h2 text-right">{{ display }}</div>
    </v-card>

    <v-row
      v-for="row in 3"
      :key="row"
      no-gutters
    >
      <v-col
        v-for="col in 3"
        :key="col"
        :order="col === 1 ? 'last' : col === 3 ? 'first' : ''"
      >
        <BtnNumber
          :value="btn[(row - 1) * 3 + col - 1]"
          @handle-click="updateDisplay"
        />
      </v-col>
    </v-row>
    <v-row>
      <v-col
        ><BtnNumber
          :value="0"
          @handle-click="updateDisplay"
      /></v-col>
      <v-col>
        <BtnNumber
          value="+"
          @handle-click="sum"
        />
      </v-col>
      <v-col>
        <BtnNumber
          value="c"
          @handle-click="resetAll"
        />
      </v-col>
      <v-col>
        <BtnNumber
          value="="
          @handle-click="calculate"
        />
      </v-col>
    </v-row>

    <ul>
      <li>num1: {{ num1 }}</li>
      <li>num2: {{ num2 }}</li>
    </ul>
  </v-container>
</template>
