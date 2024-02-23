<script setup lang="ts">
import * as z from 'zod'
import { AutoForm, AutoFormSubmit } from '../components/ui/auto-form'
import {
  Card,
  CardContent,
  CardDescription,
  CardHeader,
  CardTitle,
} from '../components/ui/card'
import { DependencyType } from '@/components/ui/auto-form/types'

const formSchema = z.object({
  age: z.number(),
  parentsAllowed: z
    .boolean()
    .describe('Did your parents allow you to register?')
    .optional(),

  vegetarian: z.boolean().optional().describe('Are you a vegetarian?'),
  mealOptions: z.enum(['Pasta', 'Salad', 'Beef Wellington']).optional(),
})
</script>

<template>
  <div class="mx-auto my-6 max-w-lg">
    <Card>
      <CardHeader>
        <CardTitle>AutoForm Dependencies</CardTitle>
        <CardDescription>
          Create dependencies between fields.
        </CardDescription>
      </CardHeader>

      <CardContent>
        <AutoForm
          :form-schema="formSchema"
          :field-config="{
            age: {
              description: 'Setting this below 18 will require parents consent.',
            },
            vegetarian: {
              description: 'Setting this to true will remove non-vegetarian food options.',
            },
            mealOptions: {
              fieldType: 'radio',
            },
          }"
          :dependencies="[
            {
              sourceField: 'age',
              type: DependencyType.HIDES,
              targetField: 'parentsAllowed',
              when: (age: number) => age >= 18,
            },
            {
              sourceField: 'age',
              type: DependencyType.REQUIRES,
              targetField: 'parentsAllowed',
              when: (age:number) => age < 18,
            },
            {
              sourceField: 'vegetarian',
              type: DependencyType.SETS_OPTIONS,
              targetField: 'mealOptions',
              when: (vegetarian: boolean) => vegetarian,
              options: ['Pasta', 'Salad'],
            },
          ]"
          @submit="console.log"
        >
          <AutoFormSubmit>Send now</AutoFormSubmit>
        </AutoForm>
      </CardContent>
    </Card>
  </div>
</template>
