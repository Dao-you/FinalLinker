<script setup lang="ts">
import { onMounted, ref } from 'vue'
import Papa from 'papaparse'
import LinkCard from './components/LinkCard.vue'

type LinkItem = { msg: string; url: string }

const CSV_URL = import.meta.env.VITE_CSV_URL as string

const links = ref<LinkItem[]>([])
const error = ref<string | null>(null)

onMounted(async () => {
  try {
    const response = await fetch(CSV_URL, { cache: 'no-store' })
    if (!response.ok) throw new Error(`HTTP ${response.status}`)
    const text = await response.text()
    const result = Papa.parse<{ name?: string; url?: string }>(text, {
      header: true,
      skipEmptyLines: true,
    })

    if (result.errors.length > 0) {
      throw new Error(result.errors[0].message)
    }

    links.value = result.data
      .map((row) => ({
        msg: (row.name || '').trim(),
        url: (row.url || '').trim(),
      }))
      .filter((link) => link.msg.length > 0 && link.url.length > 0)
  } catch (err) {
    error.value = err instanceof Error ? err.message : 'Failed to load links'
  }
})
</script>

<template>
  <div class="main-container">
    <p v-if="error" class="error-text">Failed to load links: {{ error }}</p>
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
.error-text {
  margin: 0 0 1rem;
  color: #b00020;
  font-size: 0.95rem;
}
</style>
