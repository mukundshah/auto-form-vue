<script setup lang="ts">
import { FormControl, FormItem, FormMessage } from "@/components/ui/form";
import { Textarea } from "@/components/ui/textarea";
import { AutoFormLabel, AutoFormTooltip } from "../common";

import { AutoFormInputComponentProps } from "../types";

const props = defineProps<AutoFormInputComponentProps>();

const { showLabel: _showLabel, ...fieldPropsWithoutShowLabel } = props.fieldProps;
const showLabel = _showLabel ?? true;
</script>

<template>
  <FormItem>
    <AutoFormLabel v-if="showLabel" :label="label" :required="required" />
    <FormControl>
      <Textarea v-bind="fieldPropsWithoutShowLabel" />
    </FormControl>
    <AutoFormTooltip :field-config-item="fieldConfigItem" />
    <FormMessage />
  </FormItem>
</template>
