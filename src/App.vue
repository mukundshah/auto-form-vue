<script setup lang="ts">
import Api from './examples/Api.vue'
import Array from './examples/Array.vue'
import Basics from './examples/Basics.vue'
import ConfirmPassword from './examples/ConfirmPassword.vue'
import Controlled from './examples/Controlled.vue'
import Dependencies from './examples/Dependencies.vue'
import InputWithoutLabel from './examples/InputWithoutLabel.vue'
import SubObject from './examples/SubObject.vue'
</script>

<template>
  <div class="mx-auto my-6 max-w-lg space-y-8">
    <Basics />
    <InputWithoutLabel />
    <SubObject />
    <Controlled />
    <ConfirmPassword />
    <Api />
    <Array />
    <Dependencies />
  </div>
</template>
