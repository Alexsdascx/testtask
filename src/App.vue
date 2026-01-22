<template>
  <div class="app">
    <div class="header-section">
      <SelectedItems
        title="Выбранные вещи пользователя"
        :items="selectedUserItems"
        :max="6"
      />

      <SelectedItems
        title="Выбранная вещь"
        :items="selectedAvailableItem ? [selectedAvailableItem] : []"
      />
    </div>

    <div class="content-section">
      <AvailableItems
        title="Вещи у пользователя"
        :items="userItems"
        :selected-ids="selectedUserIds"
        :max-selections="6"
        @toggle="toggleUserItem"
      />

      <AvailableItems
        title="Вещи на выбор"
        :items="availableItems"
        :selected-ids="new Set(selectedAvailableId ? [selectedAvailableId] : [])"
        :single-mode="true"
        @toggle="toggleAvailableItem"
      />
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import SelectedItems from './components/SelectedItems.vue'
import AvailableItems from './components/AvailableItems.vue'
import { userItems, availableItems } from './data/items'

const selectedUserIds = ref(new Set())
const selectedAvailableId = ref(null)

const selectedUserItems = computed(() => {
  return userItems.filter(item => selectedUserIds.value.has(item.id))
})

const selectedAvailableItem = computed(() => {
  return availableItems.find(item => item.id === selectedAvailableId.value) || null
})

function toggleUserItem(item) {
  if (selectedUserIds.value.has(item.id)) {
    selectedUserIds.value.delete(item.id)
  } else if (selectedUserIds.value.size < 6) {
    selectedUserIds.value.add(item.id)
  }
}

function toggleAvailableItem(item) {
  if (selectedAvailableId.value === item.id) {
    selectedAvailableId.value = null
  } else {
    selectedAvailableId.value = item.id
  }
}
</script>

<style>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  background: #f1f5f9;
  color: #0f172a;
  min-height: 100vh;
  padding: 20px;
}

.app {
  max-width: 1200px;
  margin: 0 auto;
}

.header-section {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 24px;
  margin-bottom: 32px;
}

.content-section {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 24px;
}

h3 {
  margin: 0;
}
</style>