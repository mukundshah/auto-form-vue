<script setup lang="ts">
import { FormControl, FormItem, FormMessage } from "@/components/ui/form";
import { Input } from "@/components/ui/input";
import { AutoFormLabel, AutoFormTooltip } from "../common";

import { AutoFormInputComponentProps } from "../types";

const props = defineProps<AutoFormInputComponentProps>();

const type = props.fieldProps.type || "text";
const { showLabel: _showLabel, ...fieldPropsWithoutShowLabel } = props.fieldProps;
const showLabel = _showLabel ?? true;
</script>

<template>
  <div class="flex flex-row  items-center space-x-2">
    <FormItem class="flex w-full flex-col justify-start">
      <AutoFormLabel v-if="showLabel" :label="label" :required="required" />
      <FormControl>
        <Input :type="type" v-bind="fieldPropsWithoutShowLabel" />
      </FormControl>
      <AutoFormTooltip :field-config-item="fieldConfigItem" />
      <FormMessage />
    </FormItem>
  </div>
</template>
