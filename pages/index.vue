<template>
  <topic-list-chalk :topicList="hotList"></topic-list-chalk>
</template>

<script>
import TopicListChalk from '~/components/TopicListChalk'

export default {
  head () {
    return {
      titleTemplate: '%s - 最热'
    }
  },
  async asyncData ({ app }) {
    const { data } = await app.$axios.get('topics/hot.json')

    return {
      hotList: data
    }
  },
  components: {
    TopicListChalk
  }
}
</script>
