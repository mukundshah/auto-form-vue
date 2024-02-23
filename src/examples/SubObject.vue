<script setup lang="ts">
import * as z from 'zod'
import { AutoForm, AutoFormSubmit } from '../components/ui/auto-form'
import {
  Card,
  CardContent,
  CardDescription,
  CardHeader,
  CardTitle,
} from '@/components/ui/card'

const formSchema = z.object({
  subObject: z.object({
    subField: z.string().optional().default('Sub Field'),
    numberField: z.number().optional().default(1),

    subSubObject: z
      .object({
        subSubField: z.string().default('Sub Sub Field'),
      })
      .describe('Sub Sub Object Description'),
  }),
  optionalSubObject: z
    .object({
      optionalSubField: z.string(),
      otherOptionalSubField: z.string(),
    })
    .optional(),
})
</script>

<template>
  <div class="mx-auto my-6 max-w-lg">
    <Card>
      <CardHeader>
        <CardTitle>Sub Object</CardTitle>
        <CardDescription>
          Automatically generate a form from a Zod schema.
        </CardDescription>
      </CardHeader>

      <CardContent>
        <AutoForm
          :form-schema="formSchema"
          :field-config="{
            subObject: {
              numberField: {
                inputProps: {
                  type: 'number',
                },
              },
            },
          }"
          @submit="console.log"
        >
          <AutoFormSubmit>Send now</AutoFormSubmit>
        </AutoForm>
      </CardContent>
    </Card>
  </div>
</template>
