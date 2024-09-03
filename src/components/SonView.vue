<script setup>
const prop = defineProps({
  message: {
    type: String,
  }
})
console.log(prop)

// 子传父 <!-- 2. @pass-data -->
const emit = defineEmits(['pass-data'])
const sendMessage = () => {
  // <!-- 3. @pass-data -->
  // 1、2、3三处函数名保持一致
  emit('pass-data', 'Message from Son')
}
</script>

<template>
  <div class="son-view">我是子组件</div>
  <div>父组件传来：{{ message }}</div>
  <button @click="sendMessage">发送</button>
</template>

<style scoped>

</style>