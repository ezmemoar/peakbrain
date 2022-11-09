<script setup lang="ts">
import { InputHTMLAttributes } from 'vue';

defineProps<{
  modelValue: string;
  label: string;
  type?: string;
}>();

defineEmits(['update:modelValue', 'enter']);
</script>

<template>
  <div>
    <label>
      {{ label }}
      <input :value="modelValue" :type="type || 'text'" @keyup.enter="$emit('enter')"
        @input="$emit('update:modelValue', ($event.target as InputHTMLAttributes).value)" />
    </label>
  </div>
</template>