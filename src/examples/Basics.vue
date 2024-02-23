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

// import { Button } from '../components/ui/button'

enum Sports {
  Football = 'Football/Soccer',
  Basketball = 'Basketball',
  Baseball = 'Baseball',
  Hockey = 'Hockey (Ice)',
  None = 'I don\'t like sports',
}

const formSchema = z.object({
  username: z
    .string({
      required_error: 'Username is required.',
    })
    .min(2, {
      message: 'Username must be at least 2 characters.',
    }),

  password: z
    .string({
      required_error: 'Password is required.',
    })
    .describe('Your secure password')
    .min(8, {
      message: 'Password must be at least 8 characters.',
    }),

  favouriteNumber: z.coerce
    .number({
      invalid_type_error: 'Favourite number must be a number.',
    })
    .min(1, {
      message: 'Favourite number must be at least 1.',
    })
    .max(10, {
      message: 'Favourite number must be at most 10.',
    })
    .default(1)
    .optional(),

  acceptTerms: z
    .boolean()
    .describe('Accept terms and conditions.')
    .refine(value => value, {
      message: 'You must accept the terms and conditions.',
      path: ['acceptTerms'],
    }),

  sendMeMails: z.boolean().optional(),

  birthday: z.coerce.date().optional(),

  color: z.enum(['red', 'green', 'blue']).optional(),

  // Another enum example
  marshmallows: z
    .enum(['not many', 'a few', 'a lot', 'too many'])
    .describe('How many marshmallows fit in your mouth?'),

  // Native enum example
  sports: z.nativeEnum(Sports).describe('What is your favourite sport?'),

  bio: z
    .string()
    .min(10, {
      message: 'Bio must be at least 10 characters.',
    })
    .max(160, {
      message: 'Bio must not be longer than 30 characters.',
    })
    .optional(),

  customParent: z.string().optional(),

  file: z.string().optional().describe('Text file'),
})
</script>

<template>
  <div class="mx-auto my-6 max-w-lg">
    <Card>
      <CardHeader>
        <CardTitle>AutoForm Example</CardTitle>
        <CardDescription>
          Automatically generate a form from a Zod schema.
        </CardDescription>
      </CardHeader>

      <CardContent>
        <AutoForm
          :form-schema="formSchema"
          :field-config="{
            password: {
              inputProps: {
                type: 'password',
                placeholder: '••••••••',
              },
            },
            favouriteNumber: {
              description: 'Your favourite number between 1 and 10.',
            },
            acceptTerms: {
              inputProps: {
                required: true,
              },
            },
            birthday: {
              description: 'We need your birthday to send you a gift.',
            },
            sendMeMails: {
              fieldType: 'switch',
            },
            bio: {
              fieldType: 'textarea',
            },
            marshmallows: {
              fieldType: 'radio',
            },
            customParent: {

            },

            file: {
              fieldType: 'file',
            },
          }"
        >
          <AutoFormSubmit>Send now</AutoFormSubmit>
        </AutoForm>
      </CardContent>
    </Card>
  </div>
</template>
