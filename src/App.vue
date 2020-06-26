<template>
  <div>
    <vote :title="title"></vote>
  </div>
</template>

<script>
import Vote from './components/Vote.vue'
export default {
  components: {
    Vote
  },
  data() {
    return {
      title: 'vue3-beta-vite'
    }
  },
  mounted() {
    setTimeout(_ => {
      this.title = 'vue 还是 react？'
    }, 1000)
  }
}
</script>
