<script setup lang="ts">
import { onMounted, ref } from 'vue'
import Papa, { type ParseResult } from 'papaparse'
import LinkCard from './components/LinkCard.vue'

type LinkItem = { msg: string; url: string }

const CSV_URL = import.meta.env.VITE_CSV_URL as string

const links = ref<LinkItem[]>([])
const error = ref<string | null>(null)

onMounted(async () => {
  try {
    console.log('CSV_URL', CSV_URL)
    const response = await fetch(CSV_URL, { cache: 'no-store' })
    if (!response.ok) throw new Error(`HTTP ${response.status}`)
    const text = await response.text()
    const result: ParseResult<{ name?: string; url?: string }> = Papa.parse(text, {
      header: true,
      skipEmptyLines: true,
    })

    const firstError = result.errors[0]
    if (firstError) {
      throw new Error(firstError.message)
    }

    links.value = result.data
      .map((row: { name?: string; url?: string }) => ({
        msg: (row.name || '').trim(),
        url: (row.url || '').trim(),
      }))
      .filter((link: LinkItem) => link.msg.length > 0 && link.url.length > 0)
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
