<template>
  <topic-list-chalk :topicList="qnaList"></topic-list-chalk>
</template>

<script>
import { fetchTopicList } from '~/utils'
import TopicListChalk from '~/components/TopicListChalk'

export default {
  head () {
    return {
      titleTemplate: '%s - 问与答'
    }
  },
  async asyncData ({ app }) {
    const nodes = ['qna']
    const qnaList = await fetchTopicList(app.$axios, nodes)

    return {
      qnaList
    }
  },
  components: {
    TopicListChalk
  }
}
</script>
