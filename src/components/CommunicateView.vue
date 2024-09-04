<script setup>
import { inject } from "vue";

// 2.接收跨多层通信数据
const received = inject('passing-to-grandson')
const receivedRef = inject('passing-ref-data')
// 接收修改数据的方法，下面直接调用
const changeRef = inject('change-message-fn')
</script>

<template>
  <div>{{ received }}</div>
  <div>{{ receivedRef }}</div>
  <button @click="changeRef">改动</button>
</template>

<style scoped>

</style>