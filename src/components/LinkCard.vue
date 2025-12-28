<script setup lang="ts">
defineProps<{
  url: string
}>()
</script>

<template>
  <a class="card" :href="url" target="_blank" rel="noopener noreferrer">
    <h2><slot></slot></h2>
    <p>{{ url }}</p>
  </a>
</template>

<style scoped>
.card {
  text-decoration: none;
  color: #540b0e;
  display: block;
  padding: 1rem 1.5rem;
  margin: 1.5rem;
  border-radius: 12px;
  text-align: left;
  transition: box-shadow 0.2s ease-in-out;
  border: 1px solid #e0a899;
  box-shadow: 0 10px 20px 0 rgba(0, 0, 0, 0.05);

  h2 {
    margin: 0;
    /* font-size: 1.5rem; */
  }

  p {
    margin: 0;
  }
}

.card:hover {
  box-shadow: 0 20px 30px 0 rgba(0, 0, 0, 0.1);
}
</style>
