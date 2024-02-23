<script setup lang="ts">
import { ref } from 'vue'

import * as z from 'zod'
import { AutoForm } from '@/components/ui/auto-form'
import {
  Card,
  CardContent,
  CardDescription,
  CardHeader,
  CardTitle,
} from '@/components/ui/card'

import { Json } from '@/components/ui/json'

const formSchema = z.object({
  guestListName: z.string(),
  invitedGuests: z
    .array(
      z.object({
        name: z.string(),
        age: z.coerce.number(),
      }),
    )
    .describe('Guests invited to the party'),
})

const formValues = ref({})
</script>

<template>
  <div class="mx-auto my-6 max-w-lg">
    <Card>
      <CardHeader>
        <CardTitle>Array support</CardTitle>
        <CardDescription>
          You can use arrays in your schemas to create dynamic forms.
        </CardDescription>
      </CardHeader>

      <CardContent>
        <AutoForm :form-schema="formSchema" :values="formValues" @submit="console.log">
          <AutoFormSubmit>Send now</AutoFormSubmit>
        </AutoForm>
        <Json :data="formValues" class="mt-6" />
      </CardContent>
    </Card>
  </div>
</template>
