<script setup lang="ts">
defineProps<{ item?: Item }>()
</script>

<template>
  <div class="item">
    {{ item?.name }}
  </div>
</template>

<style>
.item {
  height: 40px;
  display: grid;
  place-items: center;
  cursor: pointer;
  background-color: white;
  padding: 10px;
}
</style>
