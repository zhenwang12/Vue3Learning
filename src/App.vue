<script setup>
// import { reactive } from "vue";
//
// // reactive返回响应式对象
// const state = reactive({
//   count: 0
// })
// const setCount = () => {
//   state.count++
// }

import { ref, computed, watch, onMounted, provide } from "vue";
import SonView from "@/components/SonView.vue";
import ReferenceView from "@/components/ReferenceView.vue";

const count = ref(0);
const setCount = () => {
  // 必须通过.value改变值
  watchData.value++
}

const list = ref([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])
const computeState = computed(() => {
  return list.value.filter(item => {
    return item > 3
  })
})

const watchData = ref(10)
// 监听单个data
watch(watchData, (newval, oldval) => {
  console.log(`旧值是：${ oldval }, 新值是：${ newval }`);
})

// 监听多个data
const secondData = ref(-10)
watch([watchData, secondData], ([newWatch, newSecond], [oldWatch, oldSecond]) => {
      console.log(`旧值是：${ oldWatch }和${ oldSecond }, 新值是：${ newWatch }和${ newSecond }`)
    },
    // 立马触发一次回调
    { immediate: true })

// 深度监听 (deep有性能损耗，尽量不开启)
const t = ref({ age: 20, name: 'cc' })
watch(t, () => {
  console.log('t对象的属性变化了')
}, { deep: true })

// 精准监听某个属性
watch(() => t.value.age,
    () => {
      console.log('只监听age变换')
    })

const msg = ref('Father Message')
const getMessage = (msg) => {
  console.log(msg)
}

const referenceRef = ref(null)
onMounted(() => {
  console.log(referenceRef.value)
})

// 1. 跨多层通信 传递基本数据
const message = 'Basic String'
provide('passing-to-grandson', message)
// 传递响应式数据
const messageRef = ref(1000)
provide('passing-ref-data', messageRef)
// 传递的数据不能直接修改，传递修改数据的方法
const changeMessageRef = () => {
  messageRef.value++
}
provide('change-message-fn', changeMessageRef)
</script>

<template>
  <header>
    <div>{{ computeState }}</div>
  </header>

  <main>
    <button @click="setCount">{{ watchData }}</button>
    <!-- 1. @pass-data -->
    <SonView :message="msg" @pass-data="getMessage"></SonView>
    <reference-view ref="referenceRef">通信传递</reference-view>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
