<template>
  <div>
    Promised
    <slot name="error" v-if="err">{{ err }}</slot>
    <slot name="loading" v-else-if="loading"></slot>
    <slot name="default" :user="user" v-else></slot>
  </div>
</template>
<script>
import { defineComponent, onMounted, ref } from 'vue'
export default defineComponent({
  props: {
    promise: {
      type: Function,
    },
  },
  setup(props) {
    const loading = ref(false)
    const err = ref(null)
    const user = ref([])
    
    onMounted(async () => {
      try {
        loading.value = true
        const list = await props.promise()
        user.value = list
      } catch (error) {
        console.log(error)
        err.value = error
      } finally {
        loading.value = false
      }
    })

    return {
      loading,
      err,
      user,
    }
  },
})
</script>
<style lang="scss" scoped>
</style>