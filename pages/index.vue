<template>
  <div class="c-main_content top">
    <h1 class="top_title">地名を入力してください</h1>
    <div class="c-searchForm">
      <input
        v-model="searchStr"
        type="text"
        name="name"
        class="c-searchForm_text"
      />
      <button type="button" @click="submit" class="c-searchForm_button">
        検索
      </button>
    </div>
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

<style lang="scss">
.top {
  padding-top: 10vw;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  &_title {
    width: 100%;
    text-align: center;
    color: #778a99;
  }
  .c-searchForm {
    display: flex;
    &_text {
      display: block;
      padding: 1.3rem 2rem 1.3rem 5.6rem;
      border: none;
      border-radius: 2.5rem;
      box-shadow: 0 0 3rem 0 rgba(43, 86, 112, 0.1);
      color: inherit;
      font-size: 2rem;
      font-family: inherit;
      max-width: 46rem;
      width: 100%;
    }
  }
}
</style>
