<template>
  <div v-if="isLoading">
    <Spinner />
  </div>

  <div v-else>

    <div class="tweet-menu-wrapper">
      <div class="tweet-menu">
        <select v-model="sortBy" name="sortBy">
          <option value="date">Sort by date</option>
          <option value="likes">Sort by likes</option>
        </select>
      </div>
    </div>

    <div v-for="item in dataSortered" :key="item.id">
      <Tweet
          :id="item.id"
          :name="item.date"
          :likes="item.likes"
          :imgUrl="item.avatar"
          @onSubmit="handleLikeSubmit"
      >
        {{ item.body }}
      </Tweet>
    </div>
    <button @click="handleModalShow" class="btn btnTweet btnTweetHome">New tweet</button>
    <Modal title="New tweet" v-if="showModal" @onClose="handleModalShow">
      <TweetForm @onSubmit="handleTweetSubmit" />
    </Modal>
  </div>
</template>

<script>
import { ref, computed } from 'vue'
import Spinner from '@/components/UI/Spinner.vue'
import Modal from '@/components/UI/Modal.vue'
import Tweet from '@/components/UI/Tweet.vue'
import TweetForm from '@/components/UI/TweetForm.vue'

export default {
  components: {
    Spinner,
    Modal,
    Tweet,
    TweetForm
  },
  setup () {
    const data = ref([
      {
        id: 1,
        body: 'hello world',
        avatar: 'https://tocode.ru/static/_secret/bonuses/1/avatar-1Tq9kaAql.png',
        likes: 34,
        date: '10-04-2021'
      },
      {
        id: 2,
        body: 'hello world 2',
        avatar: 'https://tocode.ru/static/_secret/bonuses/1/avatar-1Tq9kaAql.png',
        likes: 0,
        date: '14-04-2021'
      },
      {
        id: 3,
        body: 'hello world 3',
        avatar: 'https://tocode.ru/static/_secret/bonuses/1/avatar-1Tq9kaAql.png',
        likes: 20,
        date: '08-04-2021'
      }
    ])

    const handleTweetSubmit = (body) => {
      data.value.push({
        id: data.value.length + 1,
        body,
        avatar: 'https://tocode.ru/static/_secret/bonuses/1/avatar-1Tq9kaAql.png',
        likes: 0,
        date: new Date(Date.now()).toLocaleString()
      });
      handleModalShow()
    }

    const handleLikeSubmit = (id) => console.log(`tweet id ${id} liked`)

    const sortBy = ref('date')
    const dataSortered = computed(() => {
      // eslint-disable-next-line vue/no-side-effects-in-computed-properties
      return data.value.sort((a,b) => {
        if (a[sortBy.value] < b[sortBy.value]) return 1
        if (a[sortBy.value] > b[sortBy.value]) return -1
      })
    })

    const isLoading = ref(false)
    // setTimeout(() => {
    //   isLoading.value = false
    // },1000)

    const showModal = ref(false)
    const handleModalShow = () => {
      const nextShowModal = showModal.value = !showModal.value
      showModal.value = nextShowModal
    }

    return { data, handleTweetSubmit, handleLikeSubmit, sortBy, dataSortered, isLoading, showModal, handleModalShow }
  }
}
</script>
