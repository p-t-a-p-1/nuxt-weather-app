<template>
  <div class="c-main_content top">
    <div class="">
      <h1 class="top_title">地名を半角英字で入力してください</h1>
      <div class="top_searchForm">
        <input
          v-model="searchStr"
          type="text"
          name="name"
          class="top_searchForm_text"
          placeholder="sapporo"
          autocomplete="off"
        />
        <button type="button" @click="submit" class="top_searchForm_button">
          <font-awesome-icon icon="search" class="-icon" />
        </button>
      </div>
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
      if (!this.searchStr.match(/^[A-Za-z0-9]*$/)) {
        return false
      }
      this.$router.push(`/city/${this.searchStr}`)
    },
  },
}
</script>

<style lang="scss" scoped>
.top {
  padding-top: 10vw;
  width: 100%;
  &_title {
    width: 100%;
    text-align: center;
    color: #778a99;
    font-size: 25px;
  }
  &_searchForm {
    padding-top: 24px;
    display: flex;
    justify-content: center;
    align-items: center;
    margin: auto;
    width: 300px;
    &_text {
      outline: none;
      width: 80%;
      height: 100%;
      display: block;
      padding: 8px 16px;
      border: none;
      border-radius: 4px;
      box-shadow: 0 0 3rem 0 rgba(43, 86, 112, 0.1);
      color: inherit;
      font-size: 2rem;
      font-family: inherit;
      &::placeholder {
        color: #d6dbe0;
      }
    }
    &_button {
      outline: none;
      margin-left: 2%;
      width: 18%;
      height: 40px;
      cursor: pointer;
      font-size: 18px;
      border-radius: 4px;
      border: none;
      color: #7fbfff;
      background-color: #fff;
      &:hover {
        opacity: 0.7;
        transition: 0.3s;
        color: #fff;
        background-color: #7fbfff;
      }
    }
  }
}
</style>
