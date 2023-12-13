<script setup lang="ts">
interface Props {
  value: number
}
const props = defineProps<Props>()

const $emit = defineEmits<{
  handleClick: [value: number]
}>()

const handleClick = () => {
  $emit('handleClick', props.value)
}
</script>

<template>
  <v-btn
    class="ma-2 btn-number"
    color="blue-grey-lighten-2"
    height="90"
    width="90"
    @click.prevent="handleClick"
  >
    <template #default>
      <h1>{{ value }}</h1>
    </template>
  </v-btn>
</template>
