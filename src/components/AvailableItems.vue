<script setup>
/* eslint-disable */
import ItemCard from './ItemCard.vue'

defineProps({
  items: {
    type: Array,
    required: true
  },
  selectedIds: {
    type: Set,
    default: () => new Set()
  },
  singleMode: {
    type: Boolean,
    default: false
  },
  maxSelections: {
    type: Number,
    default: Infinity
  },
  title: {
    type: String,
    required: true
  }
})

const emit = defineEmits(['toggle'])
</script>

<template>
  <div class="available-block">
    <h3 class="block-title">{{ title }}</h3>

    <div class="items-grid">
      <ItemCard
        v-for="item in items"
        :key="item.id"
        :item="item"
        :is-selected="selectedIds.has(item.id)"
        :disabled="singleMode
          ? selectedIds.size === 1 && !selectedIds.has(item.id)
          : selectedIds.size >= maxSelections && !selectedIds.has(item.id)"
        @click="emit('toggle', item)"
      />
    </div>
  </div>
</template>

<style scoped>
.available-block {
  padding: 20px;
  border: 1px solid #e2e8f0;
  border-radius: 12px;
  background: white;
}

.block-title {
  margin: 0 0 16px;
  font-size: 1.1rem;
  font-weight: 600;
  color: #1e293b;
}

.items-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(148px, 1fr));
  gap: 12px;
}
</style>