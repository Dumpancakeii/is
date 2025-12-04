<template>
  <input
    :value="modelValue"
    :disabled="isDisabled"
    :placeholder="placeholder"
    :data-disabled="isDisabled"
    class="ui-input"
    @input="handleInput"
    @focus="handleFocus"
    @blur="handleBlur"
  />
</template>

<script setup lang="ts">
import type { PropType } from 'vue'

// Определяем пропсы
const props = defineProps({
  modelValue: {
    type: String as PropType<string>,
    required: true
  },
  isDisabled: {
    type: Boolean as PropType<boolean>,
    default: false
  },
  placeholder: {
    type: String as PropType<string>,
    default: ''
  }
})

// Определяем эмиты
const emit = defineEmits<{
  'update:modelValue': [value: string]
  'focus': [event: FocusEvent]
  'blur': [event: FocusEvent]
}>()

// Обработчики событий
const handleInput = (event: Event) => {
  const target = event.target as HTMLInputElement
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
.ui-input {
  --input-bg: var(--ui-color-background, #ffffff);
  --input-color: var(--ui-color-text-primary, #111827);
  --input-border: var(--ui-color-border, #e5e7eb);
  --input-focus-border: var(--ui-color-border-focus, #2563eb);
  --input-disabled-bg: var(--ui-color-disabled, #f3f4f6);
  --input-disabled-color: var(--ui-color-text-disabled, #9ca3af);
  --input-placeholder-color: var(--ui-color-text-secondary, #6b7280);
  --ui-color-border-hover: var(--ui-color-border-hover, #d1d5db);
  --ui-color-focus-ring: var(--ui-color-focus-ring, rgba(37, 99, 235, 0.3));
  --ui-spacing-sm: var(--ui-spacing-sm, 0.5rem);
  --ui-spacing-md: var(--ui-spacing-md, 1rem);
  --ui-font-size-md: var(--ui-font-size-md, 1rem);
  --ui-border-radius-md: var(--ui-border-radius-md, 0.375rem);
  --ui-transition-fast: var(--ui-transition-fast, 150ms ease);

  width: 100%;
  padding: var(--ui-spacing-sm) var(--ui-spacing-md);
  font-size: var(--ui-font-size-md);
  line-height: 1.5;
  color: var(--input-color);
  background-color: var(--input-bg);
  border: 1px solid var(--input-border);
  border-radius: var(--ui-border-radius-md);
  transition: border-color var(--ui-transition-fast);
  box-sizing: border-box;
}

.ui-input::placeholder {
  color: var(--input-placeholder-color);
  opacity: 1;
}

.ui-input:focus {
  outline: none;
  border-color: var(--input-focus-border);
  box-shadow: 0 0 0 3px var(--ui-color-focus-ring);
}

.ui-input[data-disabled="true"] {
  background-color: var(--input-disabled-bg);
  color: var(--input-disabled-color);
  cursor: not-allowed;
}

.ui-input[data-disabled="true"]::placeholder {
  color: var(--input-disabled-color);
}

.ui-input:not([data-disabled="true"]):hover {
  border-color: var(--ui-color-border-hover);
}
</style>