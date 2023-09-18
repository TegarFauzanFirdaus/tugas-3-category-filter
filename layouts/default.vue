<template>
  <div id="app">
    <HeaderWeb />
    <Nuxt />
    <FooterWeb />
  </div>
</template>

<script>
// Memanggil component sesuai lokasi masing - masing file
import Header from '@/components/HeaderWeb.vue'
import Footer from '@/components/FooterWeb.vue'
export default {
  // Dideklarasikan agar dapat diakses oleh template
  components: {
    Header,
    Footer,
  },
}
</script>
<style>
body {
  background-color: rgb(42, 92, 42);
}
</style>
