<script setup lang="ts">
import { FormControl, FormItem } from "@/components/ui/form";
import { Switch } from "@/components/ui/switch";
import { AutoFormLabel, AutoFormTooltip } from "../common";

import { AutoFormInputComponentProps } from "../types";

defineProps<AutoFormInputComponentProps>();
</script>

<template>
  <div>
    <FormItem>
      <div class="flex items-center gap-3">
        <FormControl>
          <Switch :checked="field.value" @checkedChange="field.onChange" v-bind="fieldProps" />
        </FormControl>
        <AutoFormLabel :label="label" :required="required" />
      </div>
    </FormItem>
    <AutoFormTooltip :field-config-item="fieldConfigItem" />
  </div>
</template>
