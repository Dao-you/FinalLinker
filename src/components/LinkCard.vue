<script setup lang="ts">
const props = defineProps<{
  url: string
}>()

const copyUrl = async () => {
  try {
    await navigator.clipboard.writeText(props.url)
  } catch {
    const textarea = document.createElement('textarea')
    textarea.value = props.url
    textarea.setAttribute('readonly', '')
    textarea.style.position = 'absolute'
    textarea.style.left = '-9999px'
    document.body.appendChild(textarea)
    textarea.select()
    document.execCommand('copy')
    document.body.removeChild(textarea)
  }
}
</script>

<template>
  <a class="card" :href="props.url" target="_blank" rel="noopener noreferrer">
    <div class="card-left">
      <h2><slot></slot></h2>
      <p>{{ props.url }}</p>
    </div>
    <button class="card-button" type="button" aria-label="Copy link" @click.stop.prevent="copyUrl">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        width="24"
        height="24"
        viewBox="0 0 24 24"
        fill="none"
        stroke="currentColor"
        stroke-width="2"
        stroke-linecap="round"
        stroke-linejoin="round"
        class="feather feather-copy"
      >
        <rect x="9" y="9" width="13" height="13" rx="2" ry="2"></rect>
        <path d="M5 15H4a2 2 0 0 1-2-2V4a2 2 0 0 1 2-2h9a2 2 0 0 1 2 2v1"></path>
      </svg>
    </button>
  </a>
</template>

<style scoped>
.card {
  display: flex;
  flex-direction: row;
  align-items: center;
  gap: 1rem;
  text-decoration: none;
  color: #540b0e;
  padding: 1rem 1.5rem;
  margin: 1.5rem;
  border-radius: 12px;
  text-align: left;
  transition: box-shadow 0.2s ease-in-out;
  border: 1px solid #e0a899;
  box-shadow: 0 10px 20px 0 rgba(0, 0, 0, 0.05);

  &:hover {
    box-shadow: 0 20px 30px 0 rgba(0, 0, 0, 0.1);
  }

  h2 {
    margin: 0;
    /* font-size: 1.5rem; */
  }

  p {
    margin: 0;
  }

  .card-left {
    flex: 1;
    min-width: 0;

    p {
      overflow-wrap: anywhere;
    }
  }

  .card-button {
    display: flex;
    align-items: center;
    justify-content: center;
    border: 1px solid #e0a899;
    background: #ffffff;
    border-radius: 999px;
    width: 40px;
    height: 40px;
    cursor: pointer;
    color: inherit;
    padding: 0;

    &:hover {
      background: #f9f0ef;
    }
  }
}

@media (max-width: 640px) {
  .card {
    flex-direction: column;
    align-items: stretch;
  }

  .card-button {
    align-self: flex-end;
  }
}
</style>
