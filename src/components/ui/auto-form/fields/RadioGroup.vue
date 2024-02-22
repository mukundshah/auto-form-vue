<script setup lang="ts">
import { FormControl, FormItem, FormLabel, FormMessage } from "@/components/ui/form";
import { RadioGroup, RadioGroupItem } from "@/components/ui/radio-group";

import * as z from "zod";

import { AutoFormLabel, AutoFormTooltip } from "../common";

import { AutoFormInputComponentProps } from "../types";
import { getBaseSchema } from "../utils";



const props = defineProps<AutoFormInputComponentProps>();

const baseValues = (getBaseSchema(props.zodItem) as unknown as z.ZodEnum<any>)._def.values;

const values: [string, string][] = !Array.isArray(baseValues) ? Object.entries(baseValues) : baseValues.map((value) => [value, value]);
</script>

<template>
  <div>

    <FormItem>
      <AutoFormLabel :label="label" :required="required" />
      <FormControl>
        <RadioGroup v-model="field.value" v-bind="fieldProps">
          <FormItem v-for="([value, label], index) in values" :key="index" class="mb-2 flex items-center gap-3 space-y-0">
            <FormControl>
              <RadioGroupItem :value="value" />
            </FormControl>
            <FormLabel class="font-normal">{{ label }}</FormLabel>
          </FormItem>
        </RadioGroup>
      </FormControl>
      <AutoFormTooltip :field-config-item="fieldConfigItem" />
      <FormMessage />
    </FormItem>
  </div>
</template>
