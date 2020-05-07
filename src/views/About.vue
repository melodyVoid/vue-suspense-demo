<template>
  <div class="about">
    <h1>This is an about page</h1>

    <Promised :promise="fetchData">
      <template #default="{ user }">
        <!-- {{ user }} -->
        <ul>
          <li v-for="item of user" :key="item">{{ item }}</li>
        </ul>
      </template>

      <template #loading>
        Loading...
      </template>

      <template #error>
        Error
      </template>
    </Promised>
  </div>
</template>
<script>
import Promised from '../components/Promised.vue'
function timeout(ms) {
  return new Promise(resolve => setTimeout(resolve, ms))
}

async function fetchData() {
  await timeout(3000)
  // throw '错误'
  return [1, 2, 3]
}
export default {
  components: {
    Promised,
  },
  setup() {
    return {
      fetchData
    }
  }
}
</script>