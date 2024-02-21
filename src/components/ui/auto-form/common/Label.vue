<script setup lang="ts">
import { FormLabel } from "@/components/ui/form"

defineProps<{
  label: string,
  required?: boolean,
}>();
</script>

<template>
  <FormLabel>
    {{ label }}
    <span v-if="required" class="text-destructive"> *</span>
  </FormLabel>
</template>
