<template>
  <section class="container">
    <mu-text-field hintText="搜索" v-model="searchString" placeholder="搜索" />
    <mu-sub-header>
      已为您找到 {{ nodes.length }} 个节点.
    </mu-sub-header>
    <mu-chip class="chip" v-for="node in nodes" :key="node.id" @click="toNode(node.name)">
      {{ node.title }}
    </mu-chip>
  </section>
</template>

<script>
export default {
  head () {
    return {
      titleTemplate: '%s - 全部节点'
    }
  },
  async asyncData ({ app }) {
    const { data } = await app.$axios.get(`nodes/all.json`)

    return {
      nodeList: data
    }
  },
  data () {
    return {
      searchString: ''
    }
  },
  methods: {
    toNode (name) {
      this.$router.push(`/node/${name}`)
    }
  },
  computed: {
    nodes () {
      if (!this.searchString) return this.nodeList

      let searchString = this.searchString.trim().toLowerCase()

      return this.nodeList.filter(({ title, name }) =>
        title.toLowerCase().indexOf(searchString) !== -1 ||
        name.toLowerCase().indexOf(searchString) !== -1
      )
    }
  },
  layout: 'mobile'
}
</script>

<style lang="scss" scoped>
.mu-input {
  width: 100%;
  margin: 20px 0 0;
  padding: 0 10px;
}
</style>
