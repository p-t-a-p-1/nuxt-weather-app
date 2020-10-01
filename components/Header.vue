<template>
  <header class="c-header">
    <nuxt-link class="c-header_logo" to="/">WEATHER</nuxt-link>
    <!-- <nav class="c-header_nav">
      <button class="c-header_nav_menu">
        <span class="-line01"></span>
        <span class="-line02"></span>
        <span class="-line03"></span>
      </button>
      <div class="c-header_nav_wrap">
        <ul class="c-header_nav_link">
          <li class="-home">HOME</li>
        </ul>
      </div>
    </nav> -->
  </header>
</template>

<style lang="scss">
.c-header {
  // TODO mixinが使えない
  // @include flex(center, center);
  display: flex;
  align-items: center;
  justify-content: center;
  height: 80px;
  &_logo {
    font-size: 4.5rem;
    font-weight: bold;
    color: #333;
  }
}
</style>
