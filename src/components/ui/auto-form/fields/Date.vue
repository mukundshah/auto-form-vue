<script setup lang="ts">
import { FormControl, FormItem, FormMessage } from "@/components/ui/form";
import { DatePicker } from "@/components/ui/date-picker";
import { AutoFormLabel, AutoFormTooltip } from "../common";

import { AutoFormInputComponentProps } from "../types";

defineProps<AutoFormInputComponentProps>();
</script>

<template>
  <FormItem>
    <AutoFormLabel :label="label" :required="required" />
    <FormControl>
      <DatePicker :date="field.value" :set-date="field.onChange" v-bind="fieldProps" />
    </FormControl>
    <AutoFormTooltip :field-config-item="fieldConfigItem" />
    <FormMessage />
  </FormItem>
</template>
