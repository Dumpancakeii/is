<template>
  <div class="ui-field">
    <label v-if="label" class="ui-field__label">
      {{ label }}
    </label>
    <div class="ui-field__content">
      <slot />
    </div>
    <div v-if="hasError" class="ui-field__error">
      {{ error }}
    </div>
    <div v-if="description" class="ui-field__description">
      {{ description }}
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue'

// Определяем пропсы с интерфейсом
interface Props {
  label?: string
  error?: string
  description?: string
}

const props = withDefaults(defineProps<Props>(), {
  label: '',
  error: '',
  description: ''
})

// Вычисляемое свойство для проверки наличия ошибки
const hasError = computed(() => {
  return Boolean(props.error && props.error.trim().length > 0)
})
</script>

<style scoped>
.ui-field {
  --field-label-color: var(--ui-color-text-primary, #111827);
  --field-error-color: var(--ui-color-danger, #ef4444);
  --field-description-color: var(--ui-color-text-secondary, #6b7280);
  --ui-spacing-xs: var(--ui-spacing-xs, 0.25rem);
  --ui-font-size-sm: var(--ui-font-size-sm, 0.875rem);
  --ui-font-size-xs: var(--ui-font-size-xs, 0.75rem);
  --ui-font-weight-medium: var(--ui-font-weight-medium, 500);

  display: flex;
  flex-direction: column;
  gap: var(--ui-spacing-xs);
  width: 100%;
}

.ui-field__label {
  font-size: var(--ui-font-size-sm);
  font-weight: var(--ui-font-weight-medium);
  color: var(--field-label-color);
  user-select: none;
  line-height: 1.25;
}

.ui-field__content {
  display: flex;
  flex-direction: column;
  gap: var(--ui-spacing-xs);
}

.ui-field__error {
  font-size: var(--ui-font-size-xs);
  color: var(--field-error-color);
  margin-top: calc(var(--ui-spacing-xs) / 2);
  line-height: 1.25;
}

.ui-field__description {
  font-size: var(--ui-font-size-xs);
  color: var(--field-description-color);
  margin-top: calc(var(--ui-spacing-xs) / 2);
  line-height: 1.25;
  font-style: italic;
}
</style>