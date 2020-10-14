<template>
  <div class="c-main_content error">
    <div class="error_wrap">
      <h2 class="error_wrap_subtitle">お探しの地域が見つかりませんでした。</h2>
      <ul class="error_wrap_list">
        <li class="-item -home">
          <nuxt-link to="/" class="-link">検索画面へ</nuxt-link>
        </li>
        <li class="-item">
          <nuxt-link to="/" class="-link">札幌市の天気</nuxt-link>
        </li>
        <li class="-item">
          <nuxt-link to="/city/tokyo" class="-link">東京都の天気</nuxt-link>
        </li>
        <li class="-item">
          <nuxt-link to="/city/osaka" class="-link">大阪府の天気</nuxt-link>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  props: ['error'],
}
</script>

<style lang="scss" scoped>
.error {
  &_wrap {
    color: #778a99;
    &_subtitle {
      margin-top: 30px;
      font-size: 2rem;
    }
    &_list {
      margin-top: 30px;
      .-item {
        &.-home {
          font-size: 3rem;
          font-weight: bold;
        }
        &:nth-of-type(n + 2) {
          margin-top: 10px;
        }
      }
      .-link {
        color: #778a99;
        &:hover {
          opacity: 0.8;
        }
      }
    }
  }
}
</style>
