<script setup lang="ts">
import { FormControl, FormItem, FormMessage } from "@/components/ui/form";
import { Input } from "@/components/ui/input";
import { Trash2 } from "lucide-vue-next";
import { AutoFormLabel, AutoFormTooltip } from "../common";

import { AutoFormInputComponentProps } from "../types";
import { ref } from "vue";

const props = defineProps<AutoFormInputComponentProps>();

const { showLabel: _showLabel, ...fieldPropsWithoutShowLabel } = props.fieldProps;
const showLabel = _showLabel ?? true;

const file = ref<string | null>(null);
const fileName = ref<string | null>(null);

const handleFileChange = (event: Event) => {
  const file = event.target.files?.[0];

  if (file) {
    const reader = new FileReader();
    reader.onloadend = () => {
      file.value = reader.result as string;
      fileName.value = file.name;
      props.field.onChanged(reader.result as string);
    };
    reader.readAsDataURL(file);
  }
};

const handleRemoveFile = () => {
  file.value = null;
  fileName.value = null;
};
</script>

<template>
  <FormItem>
    <AutoFormLabel v-if="showLabel" :label="label" :required="required" />
    <FormControl>
      <Input :type="file" v-bind="fieldPropsWithoutShowLabel" @change="handleFileChange" :value="''" />
    </FormControl>
    <template v-if="file">
      <div
        class="flex h-[40px] w-full flex-row items-center justify-between space-x-2 rounded-sm border p-2 text-black focus-visible:ring-0 focus-visible:ring-offset-0 dark:bg-white dark:text-black dark:focus-visible:ring-0 dark:focus-visible:ring-offset-0">
        <p>{{ fileName }}</p>
        <button type="button" @click="handleRemoveFile" aria-label="Remove file">
          <Trash2 :size="16" />
        </button>
      </div>
    </template>
    <AutoFormTooltip :field-config-item="fieldConfigItem" />
    <FormMessage />
  </FormItem>
</template>
