<template>
  <div>
    <Header />
    <main class="c-main">
      <Nuxt />
    </main>
  </div>
</template>

<style lang="scss">
.c {
  &-main {
    margin: auto;
    max-width: 1280px;
  }
}
</style>

<script>
import Header from '@/components/Header.vue'
export default {
  components: {
    Header,
  },
}
</script>
