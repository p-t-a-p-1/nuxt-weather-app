<template>
  <div class="c-main_content top">
    <h1 class="top_title">地名を入力してください</h1>
    <div class="searchForm">
      <input
        v-model="searchStr"
        type="text"
        name="name"
        class="searchForm_text"
      />
      <button type="button" @click="submit" class="searchForm_button">
        <font-awesome-icon icon="search" class="-icon" />
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

<style lang="scss" scoped>
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
  .searchForm {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 300px;
    height: 50px;
    &_text {
      display: block;
      padding: 8px 16px;
      border: none;
      border-radius: 2.5rem;
      box-shadow: 0 0 3rem 0 rgba(43, 86, 112, 0.1);
      color: inherit;
      font-size: 2rem;
      font-family: inherit;
      width: 80%;
    }
    &_button {
      width: 20%;
      height: 100%;
      cursor: pointer;
      color: #778a99;
      border: none;
      background: none;
      &:hover {
        opacity: 0.7;
        transition: 0.3s;
        border: 1px solid #778a99;
        border-radius: 100%;
      }
    }
  }
}
</style>
