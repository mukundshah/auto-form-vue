<script setup lang="ts">
import { cn } from "@/lib/utils"
import type { HTMLAttributes } from "vue"

const props = defineProps<{ data: any, class?: HTMLAttributes["class"] }>()
</script>

<template>
  <div :class="cn('rounded-lg p-3 bg-zinc-100 font-mono', props.class)">
    <pre class="text-sm">{{ JSON.stringify(data, null, 2) }}</pre>
  </div>
</template>
