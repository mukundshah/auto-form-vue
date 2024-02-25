<script setup lang="ts">
import { useForm, useFormContext } from 'react-hook-form'
import type * as z from 'zod'
import { DEFAULT_ZOD_HANDLERS, INPUT_COMPONENTS } from '../config'
import type { FieldConfig } from '../types'
import { Dependency, FieldConfigItem } from '../types'
import {
  beautifyObjectName,
  getBaseSchema,
  getBaseType,
  zodToHtmlInputProps,
} from '../utils'
import resolveDependencies from '../dependencies'
import AutoFormArray from './array'
import { FormField } from '@/components/ui/form'
import {
  Accordion,
  AccordionContent,
  AccordionItem,
  AccordionTrigger,
} from '@/components/ui/accordion'
</script>

<template>
  <Accordion type="multiple" class="space-y-5 border-none">
    <!-- <AccordionItem v-for="(item, name) in shape" :key="name" :value="name" class="border-none">
      <AccordionTrigger>{{ item._def.description ?? beautifyObjectName(name) }}</AccordionTrigger>
      <AccordionContent class="p-2">
        <AutoFormObject
          :schema="(item as unknown as z.ZodObject<any, any>)"
          :form="form"
          :field-config="(fieldConfig?.[name] as FieldConfig<z.infer<typeof item>>)"
          :path="[...path, name]"
        />
      </AccordionContent>
    </AccordionItem> -->
  </Accordion>
</template>
