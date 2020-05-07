<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png" /> -->

    <div v-if="error">{{ error }}</div>
    <Suspense v-else>
      <template #default>
        <AsyncComponent></AsyncComponent>
      </template>

      <template #fallback>
        <span>Loading...</span>
      </template>
    </Suspense>
  </div>
</template>

<script>
// @ is an alias to /src
import { onErrorCaptured, ref } from 'vue'

import AsyncComponent from '../components/AsyncComponent.vue'

export default {
  name: 'Home',
  components: {
    AsyncComponent,
  },
  setup() {
    const error = ref(null)
    onErrorCaptured(err => {
      error.value = err
      return true
    })

    return {
      error,
    }
  },
}
</script>
