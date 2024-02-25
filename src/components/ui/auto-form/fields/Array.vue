<script setup lang="ts">
import { Plus, Trash } from 'lucide-vue-next'
import { AutoFormLabel, AutoFormTooltip } from '../common'
import type { AutoFormInputComponentProps } from '../types'
import {
  AccordionContent,
  AccordionItem,
  AccordionTrigger,
} from '@/components/ui/accordion'
import { Button } from '@/components/ui/button'
import { Separator } from '@/components/ui/separator'
import { FormControl, FormItem, FormMessage } from '@/components/ui/form'
import { Input } from '@/components/ui/input'

const props = defineProps<AutoFormInputComponentProps>()

const type = props.fieldProps.type || 'text'
const { showLabel: _showLabel, ...fieldPropsWithoutShowLabel } = props.fieldProps
const showLabel = _showLabel ?? true
</script>

<template>
  <div class="flex flex-row  items-center space-x-2">
    <FormItem class="flex w-full flex-col justify-start">
      <AutoFormLabel v-if="showLabel" :label="label" :required="required" />
      <FormControl>
        <Input :type="type" v-bind="fieldPropsWithoutShowLabel" />
      </FormControl>
      <AutoFormTooltip :field-config-item="fieldConfigItem" />
      <FormMessage />
    </FormItem>
  </div>
</template>
