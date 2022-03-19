<template>
  <div v-if="isLoading">
    <Spinner />

    <button class="btn">
      <Spinner :width="18" :height="18" v-if="isLoading"/>
      <span v-else>Submit</span>
    </button>
  </div>
  <div v-else>
    Content
  </div>
</template>

<script>
import {ref} from 'vue'
import Spinner from '@/components/UI/Spinner.vue'

export default {
  components: {
    Spinner
  },
  setup() {
    const isLoading = ref(true)

    setTimeout(() => {
      isLoading.value = false
    }, 2000)

    return { isLoading }
  }
}
</script>

<style scoped>

</style>
