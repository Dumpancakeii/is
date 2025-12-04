<template>
  <select
    :value="modelValue"
    :disabled="isDisabled"
    :data-disabled="isDisabled"
    class="ui-select"
    @change="handleChange"
    @focus="handleFocus"
    @blur="handleBlur"
  >
    <option 
      v-if="placeholder" 
      value="" 
      disabled
      :selected="!modelValue"
    >
      {{ placeholder }}
    </option>
    <option
      v-for="option in options"
      :key="option"
      :value="option"
      :selected="modelValue === option"
    >
      {{ option }}
    </option>
  </select>
</template>

<script setup lang="ts">
import { defineProps, defineEmits, withDefaults } from 'vue'


interface Props {
  modelValue: string
  isDisabled?: boolean
  options: string[]
  placeholder?: string
}


const props = withDefaults(defineProps<Props>(), {
  isDisabled: false,
  placeholder: '',
  options: () => []
})


const emit = defineEmits<{
  'update:modelValue': [value: string]
  'focus': [event: FocusEvent]
  'blur': [event: FocusEvent]
}>()


const handleChange = (event: Event) => {
  const target = event.target as HTMLSelectElement
  emit('update:modelValue', target.value)
}

const handleFocus = (event: FocusEvent) => {
  emit('focus', event)
}

const handleBlur = (event: FocusEvent) => {
  emit('blur', event)
}
</script>

<style scoped>
.ui-select {
  --select-bg: var(--ui-color-background, #ffffff);
  --select-color: var(--ui-color-text-primary, #111827);
  --select-border: var(--ui-color-border, #e5e7eb);
  --select-focus-border: var(--ui-color-border-focus, #2563eb);
  --select-disabled-bg: var(--ui-color-disabled, #f3f4f6);
  --select-disabled-color: var(--ui-color-text-disabled, #9ca3af);
  --ui-color-border-hover: var(--ui-color-border-hover, #d1d5db);
  --ui-color-focus-ring: var(--ui-color-focus-ring, rgba(37, 99, 235, 0.3));
  --ui-color-text-primary: var(--ui-color-text-primary, #111827);
  --ui-color-text-disabled: var(--ui-color-text-disabled, #9ca3af);
  --ui-spacing-sm: var(--ui-spacing-sm, 0.5rem);
  --ui-spacing-md: var(--ui-spacing-md, 1rem);
  --ui-spacing-xl: var(--ui-spacing-xl, 2rem);
  --ui-font-size-md: var(--ui-font-size-md, 1rem);
  --ui-border-radius-md: var(--ui-border-radius-md, 0.375rem);
  --ui-transition-fast: var(--ui-transition-fast, 150ms ease);

  width: 100%;
  padding: var(--ui-spacing-sm) var(--ui-spacing-md);
  padding-right: var(--ui-spacing-xl);
  font-size: var(--ui-font-size-md);
  line-height: 1.5;
  color: var(--select-color);
  background-color: var(--select-bg);
  border: 1px solid var(--select-border);
  border-radius: var(--ui-border-radius-md);
  cursor: pointer;
  appearance: none;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' fill='none' viewBox='0 0 20 20'%3E%3Cpath stroke='%236b7280' stroke-linecap='round' stroke-linejoin='round' stroke-width='1.5' d='m6 8 4 4 4-4'/%3E%3C/svg%3E");
  background-repeat: no-repeat;
  background-position: right 0.5rem center;
  background-size: 1.5em 1.5em;
  transition: border-color var(--ui-transition-fast);
  box-sizing: border-box;
}

.ui-select:focus {
  outline: none;
  border-color: var(--select-focus-border);
  box-shadow: 0 0 0 3px var(--ui-color-focus-ring);
}

.ui-select[data-disabled="true"] {
  background-color: var(--select-disabled-bg);
  color: var(--select-disabled-color);
  cursor: not-allowed;
  opacity: 0.7;
}

.ui-select:not([data-disabled="true"]):hover {
  border-color: var(--ui-color-border-hover);
}

.ui-select option {
  color: var(--ui-color-text-primary);
  background-color: var(--ui-color-background, #ffffff);
}

.ui-select option:disabled {
  color: var(--ui-color-text-disabled);
}


.ui-select::-ms-expand {
  display: none;
}


.ui-select {
  -moz-appearance: none;
  -webkit-appearance: none;
}


.ui-select::-ms-expand {
  display: none;
}
</style>