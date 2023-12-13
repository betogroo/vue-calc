<script setup lang="ts">
import { BtnNumber } from '../components'

const setNumber = (value: number) => {
  console.log(value)
}

const btn = [9, 8, 7, 6, 5, 4, 3, 2, 1]
</script>
<template>
  <v-container class="ma-0 pa-0">
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
          @handle-click="setNumber"
        />
      </v-col>
    </v-row>
    <v-row>
      <v-col
        ><BtnNumber
          :value="0"
          @handle-click="setNumber"
      /></v-col>
    </v-row>
  </v-container>
</template>
