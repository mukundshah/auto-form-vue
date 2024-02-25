<script setup lang="ts">
import { Button } from '@/components/ui/button'
</script>

<template>
  <Button type="submit">
    <slot>
      Submit
    </slot>
  </Button>
</template>
