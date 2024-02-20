<script setup lang="ts">
import { AutoFormSubmit } from '@/components/ui/auto-form'
</script>

<template>
  <div class="mx-auto my-6 max-w-lg space-y-8">
    <AutoFormSubmit />
  </div>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}

.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}

.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
