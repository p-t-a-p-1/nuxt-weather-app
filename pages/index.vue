<template>
  <div class="c-contents">
    <h1>test</h1>
    <ul>
      <li><nuxt-link :to="`city/sapporo/`">Sapporo</nuxt-link></li>
    </ul>
    <input v-model="searchStr" type="text" name="name" />
    <button type="button" @click="submit">検索</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchStr: '',
    }
  },
  methods: {
    // 地名検索
    submit() {
      this.$router.push(`/city/${this.searchStr}`)
    },
  },
}
</script>
