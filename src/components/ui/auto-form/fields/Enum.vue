<script setup lang="ts">
import { FormControl, FormItem, FormMessage } from "@/components/ui/form";
import {
  SelectContent,
  SelectItem,
  SelectTrigger,
  SelectValue,
} from "@/components/ui/select";
import * as z from "zod";

import { AutoFormLabel, AutoFormTooltip } from "../common";

import { AutoFormInputComponentProps } from "../types";
import { getBaseSchema } from "../utils";



const props = defineProps<AutoFormInputComponentProps>();

const baseValues = (getBaseSchema(props.zodItem) as unknown as z.ZodEnum<any>)._def.values;

let values: [string, string][] = !Array.isArray(baseValues) ? Object.entries(baseValues) : baseValues.map((value) => [value, value]);


const findItem = (value: any) => {
  return values.find((item) => item[0] === value);
}

</script>

<template>
  <FormItem>
    <AutoFormLabel :label="label" :required="required" />
    <FormControl>
      <Select v-model="field.value" v-bind="fieldProps">
        <SelectTrigger :class="fieldProps.class">
          <SelectValue>
            {{ field.value ? findItem(field.value)?.[1] : "Select an option" }}
          </SelectValue>
        </SelectTrigger>
        <SelectContent>
          <SelectItem v-for="([value, label], index) in values" :key="index" :value="value">
            {{ label }}
          </SelectItem>
        </SelectContent>
      </Select>
    </FormControl>
    <AutoFormTooltip :field-config-item="fieldConfigItem" />
    <FormMessage />
  </FormItem>
</template>
