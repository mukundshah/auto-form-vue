<script setup lang="ts">
import * as z from 'zod'
import { ref, watchEffect } from 'vue'
import { AutoForm } from '../components/ui/auto-form'
import {
  Card,
  CardContent,
  CardDescription,
  CardHeader,
  CardTitle,
} from '../components/ui/card'

const formSchema = z.object({
  username: z.string(),
})

const values = ref<Partial<z.infer<typeof formSchema>>>({})

watchEffect(() => {
  // eslint-disable-next-line no-console
  console.log(values.value)
})
</script>

<template>
  <div class="mx-auto my-6 max-w-lg">
    <Card>
      <CardHeader>
        <CardTitle>Controlled</CardTitle>
        <CardDescription>
          This example shows how to use AutoForm in a controlled way.
        </CardDescription>
      </CardHeader>

      <CardContent>
        <AutoForm :form-schema="formSchema" :values="values" />
      </CardContent>
    </Card>
  </div>
</template>
