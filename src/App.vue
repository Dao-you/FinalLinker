<script setup lang="ts">
import LinkCard from './components/LinkCard.vue'

const links = [
  { url: 'https://links.cppc.tw', msg: '測試' },
  { url: 'https://links.cppc.tw', msg: '測試' },
]
</script>

<template>
  <div class="main-container">
    <LinkCard url="https://links.cppc.tw"> 測試 </LinkCard>
    <LinkCard url="https://links.cppc.tw"> 測試 </LinkCard>
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
}
</style>
