<script setup>
import { onMounted, ref } from "vue";
// 1. 声明
const h1Ref = ref(null)

// 3. 挂载之后可以调用
onMounted(() => {
  console.log("Component mounted", h1Ref.value)
})

// 组件内部属性和方法默认不开放给父组件，需要用defineExpose
const reCount = ref(101)
const changeCount = () => {
  console.log(reCount.value)
}
// 在父组件中用ref可以获取暴露的属性和方法
defineExpose({
  reCount,
  changeCount
})
</script>

<template>
  <!--2、绑定ref-->
  <h1 ref="h1Ref">我是h1标签</h1>
</template>

<style scoped>

</style>