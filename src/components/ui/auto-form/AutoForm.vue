<script setup lang="ts">
import { h } from 'vue'
import { useForm } from 'vee-validate'
import { toTypedSchema } from '@vee-validate/zod'
import * as z from 'zod'
import type { HTMLAttributes } from 'vue'
import { AutoFormObject } from './fields'
import { Form } from '@/components/ui/form'
import { cn } from '@/lib/utils'

const props = defineProps<{
  class?: HTMLAttributes['class']
}>()

const form = useForm({
  validationSchema: toTypedSchema(
    z.object({
      name: z.string().nonempty(),
      email: z.string().email(),
      message: z.string().nonempty(),
    }),
  ),
})








</script>

<template>
  <div class="w-full">
    <Form v-bind="form">
      <form :class="cn('space-y-5', props.class)" @submit="form.handleSubmit">
        <AutoFormObject />
        <slot></slot>
      </form>
    </Form>
  </div>
</template>
