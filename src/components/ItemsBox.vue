<script setup lang="ts">
import Item from '@/components/ItemOne.vue'

withDefaults(defineProps<{ items: Item[]; selectedItems?: Set<Item> }>(), {
  selectedItems: () => new Set(),
})
const emits = defineEmits(['item-click'])
</script>

<template>
  <ul>
    <template
      v-for="(item, key) in items"
      :key="item.id + key"
    >
      <li
        v-show="!selectedItems.has(item)"
        @click="emits('item-click', item as Item)"
      >
        <Item :item="item" />
      </li>
    </template>
  </ul>
</template>

<style lang="scss">
ul {
  width: 100%;
  height: 100%;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  align-content: start;
  gap: 5px;
  list-style-type: none;
  background-color: grey;
  padding: 10px;
}
</style>
