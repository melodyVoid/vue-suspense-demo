<template>
  <div>
    <ul>
      <li v-for="item in list" :key="item">{{ item }}</li>
    </ul>
  </div>
</template>
<script>
import { defineComponent } from 'vue'

function timeout(ms) {
  return new Promise(resolve => setTimeout(resolve, ms))
}

async function fetchData() {
  await timeout(3000)
  // throw '错误'
  return [1, 2, 3]
}

export default defineComponent({
  props: {},
  async setup() {
    const list = await fetchData()
    return { list }
  },
})
</script>
<style lang="scss" scoped></style>
