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
    <button @click="handleModalShow" class="btn btnPrimary">Open modal</button>
    <Modal v-if="showModal" @onClose="handleModalShow">
      example modal
    </Modal>
  </div>
</template>

<script>
import {ref} from 'vue'
import Spinner from '@/components/UI/Spinner.vue'
import Modal from '@/components/UI/Modal.vue'

export default {
  components: {
    Spinner,
    Modal
  },
  setup() {
    const isLoading = ref(false)




    const showModal = ref(false)
    const handleModalShow = () => {
      const nextShowModal = showModal.value = !showModal.value
      showModal.value = nextShowModal
    }
    // setTimeout(() => {
    //   isLoading.value = false
    // }, 2000)

    return { isLoading, showModal, handleModalShow }
  }
}
</script>

<style scoped>

</style>
