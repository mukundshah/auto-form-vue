<script setup lang="ts">
import { onMounted, ref } from 'vue'

import * as z from 'zod'
import { AutoForm } from '@/components/ui/auto-form'
import {
  Card,
  CardContent,
  CardDescription,
  CardHeader,
  CardTitle,
} from '@/components/ui/card'

const formSchema = ref<z.ZodObject<any, any, any> | null>(null)

onMounted(async () => {
  const response = await fetch('https://jsonplaceholder.typicode.com/users')
  const data = await response.json()

  const schema = z.object({
    user: z.enum(data.map((user: any) => user.name)),
  })

  // @ts-expect-error not sure why this is happening
  formSchema.value = schema
})
</script>

<template>
  <div class="mx-auto my-6 max-w-lg">
    <Card>
      <CardHeader>
        <CardTitle>API Example</CardTitle>
        <CardDescription>
          The form select options are fetched from an API.
        </CardDescription>
      </CardHeader>

      <CardContent>
        <AutoForm :form-schema="formSchema" @submit="console.log" />
      </CardContent>
    </Card>
  </div>
</template>
