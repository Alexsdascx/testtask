<template>
  <div
    class="item-card"
    :class="{ selected: isSelected, disabled }"
    @click="!disabled && emit('click', item)"
  >
    <div class="item-name">{{ item.name }}</div>
    <div class="item-id">ID: {{ item.id }}</div>
  </div>
</template>

<script setup>
/* eslint-disable */
defineProps({
  item: {
    type: Object,
    required: true
  },
  isSelected: {
    type: Boolean,
    default: false
  },
  disabled: {
    type: Boolean,
    default: false
  }
})

const emit = defineEmits(['click'])
</script>


<style scoped>
.item-card {
  padding: 14px 16px;
  border: 1px solid #cbd5e1;
  border-radius: 10px;
  cursor: pointer;
  transition: all 0.15s ease;
  user-select: none;
  background: white;
}

.item-card:hover:not(.disabled):not(.selected) {
  border-color: #3b82f6;
  background: #f0f7ff;
  box-shadow: 0 1px 3px rgba(0,0,0,0.08);
}

.item-card.selected {
  border-color: #2563eb;
  background: #eff6ff;
  font-weight: 500;
}

.item-card.disabled {
  opacity: 0.55;
  cursor: not-allowed;
  background: #f8fafc;
}

.item-name {
  font-size: 15px;
  margin-bottom: 5px;
}

.item-id {
  font-size: 12.5px;
  color: #64748b;
}
</style>