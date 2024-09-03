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

import { ref, computed, watch } from "vue";

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
</script>

<template>
  <header>
    <div>{{ computeState }}</div>
  </header>

  <main>
    <button @click="setCount">{{ watchData }}</button>
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
