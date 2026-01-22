
<template>
  <div class="selected-block">
    <h3 class="block-title">
      {{ title }}
      <span v-if="max < Infinity" class="count">({{ items.length }} / {{ max }})</span>
    </h3>

    <div v-if="!items.length" class="empty">
      Ничего не выбрано
    </div>

    <div v-else class="selected-list">
      <div
        v-for="item in items"
        :key="item.id"
        class="selected-item"
      >
        {{ item.name }}
      </div>
    </div>
  </div>
</template>

<script setup>
/* eslint-disable */
defineProps({
  items: {
    type: Array,
    default: () => []
  },
  title: {
    type: String,
    required: true
  },
  max: {
    type: Number,
    default: Infinity
  }
})
</script>


<style scoped>
.selected-block {
  padding: 20px;
  border: 1px solid #cbd5e1;
  border-radius: 12px;
  background: #f8fafc;
  min-height: 148px;
}

.block-title {
  margin: 0 0 14px;
  font-size: 1.1rem;
  font-weight: 600;
  color: #1e293b;
}

.count {
  font-size: 0.9rem;
  color: #64748b;
  font-weight: normal;
}

.selected-list {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

.selected-item {
  padding: 6px 14px;
  background: #e0f2fe;
  border: 1px solid #bae6fd;
  border-radius: 8px;
  font-size: 14px;
}

.empty {
  color: #94a3b8;
  font-style: italic;
  text-align: center;
  padding: 32px 0;
}
</style>