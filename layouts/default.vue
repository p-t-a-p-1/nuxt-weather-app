<template>
  <div>
    <Header />
    <main class="main">
      <Nuxt />
    </main>
  </div>
</template>

<style></style>

<script>
import Header from '@/components/Header.vue'
export default {
  components: {
    Header,
  },
}
</script>
