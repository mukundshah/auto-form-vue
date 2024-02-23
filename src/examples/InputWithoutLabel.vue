<script setup lang="ts">
import * as z from 'zod'
import { AutoForm } from '../components/ui/auto-form'
import {
  Card,
  CardContent,
  CardDescription,
  CardHeader,
  CardTitle,
} from '../components/ui/card'
import { Button } from '@/components/ui/button'

const formSchema = z.object({
  username: z.string(),
})
</script>

<template>
  <div class="mx-auto my-6 max-w-lg">
    <Card>
      <CardHeader>
        <CardTitle>Input Without Label</CardTitle>
        <CardDescription>
          This example shows how to use AutoForm input without label.
        </CardDescription>
      </CardHeader>

      <CardContent>
        <AutoForm
          :form-schema="formSchema" :field-config="{
            username: {
              inputProps: {
                showLabel: false,
                placeholder: 'Username',
              },
            },
          }"
        >
          <template #username="{ children }">
            <div class="flex items-end gap-3">
              <div class="flex-1">
                {{
                  children
                }}
              </div>
              <div>
                <Button type="button">
                  Update
                </Button>
              </div>
            </div>
          </template>
        </AutoForm>
      </CardContent>
    </Card>
  </div>
</template>
