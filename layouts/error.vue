<template>
  <div class="c-main_content">
    <div class="c-main_content_notfound">
      <h1 class="-title">Page Not Found...</h1>
      <h2 class="-subtitle">お探しのページが見つかりませんでした。</h2>
      <ul class="-list">
        <li class="-item">
          <nuxt-link to="/" class="-link">ホーム</nuxt-link>
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

<style lang="scss">
.c {
  &-main {
    &_content {
      &_notfound {
        .-title {
          font-size: 3rem;
        }
        .-subtitle {
          margin-top: 30px;
          font-size: 2rem;
        }
        .-list {
          margin-top: 30px;
        }
        .-item {
          &:nth-of-type(n + 2) {
            margin-top: 10px;
          }
        }
        .-link {
          color: #333;
          &:hover {
            opacity: 0.8;
          }
        }
      }
    }
  }
}
</style>
