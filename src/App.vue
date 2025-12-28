<script setup lang="ts">
import LinkCard from './components/LinkCard.vue'

const links = [
  { msg: 'Canva', url: 'https://www.canva.com/design/DAG8nW1kj-A/hbwxja5j_ULsZ8VcaTQWPg/view' },
  {
    msg: 'PDF',
    url: 'https://1drv.ms/f/c/50640dcb5cd6ab7a/IgC0wHSnYYcuQYVcMTtQSb0kARGilb2Ru-E8VG4KsMV776k?e=TX8Mgw',
  },
  { msg: 'Github', url: 'https://github.com/Dao-you/BetterRDPLauncher' },
]
</script>

<template>
  <div class="main-container">
    <LinkCard v-for="(link, index) in links" :key="index" :url="link.url">
      {{ link.msg }}
      <!-- <template #url>{{ link.url }}</template> -->
    </LinkCard>
  </div>
</template>

<style>
body {
}
.main-container {
  width: 100vw;
  max-width: 720px;
  margin: 0 auto;
  padding: 2rem;
  font-family: sans-serif;
}
</style>
