<script setup lang="ts">
defineProps<{ fieldConfigItem: any }>();
</script>

<template>
  <p v-if="fieldConfigItem?.description" class="ext-sm text-gray-500 dark:text-white">
    {{ fieldConfigItem.description }}
  </p>
</template>
