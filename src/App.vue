<script setup lang="ts">
import { reactive } from 'vue'
import Item from '@/components/ItemOne.vue'
import ItemsBox from '@/components/ItemsBox.vue'

const items = {
  left: [
    {
      id: 1,
      name: 'Shoes 1',
    },
    {
      id: 2,
      name: 'Shoes 2',
    },
    {
      id: 3,
      name: 'Shoes 3',
    },
    {
      id: 4,
      name: 'Shoes 4',
    },
    {
      id: 5,
      name: 'T-shirt 1',
    },
    {
      id: 6,
      name: 'T-shirt 2',
    },
    {
      id: 7,
      name: 'T-shirt 3',
    },
    {
      id: 8,
      name: 'T-shirt 4',
    },
  ],
  right: [
    {
      id: 11,
      name: 'Jacket 1',
    },
    {
      id: 12,
      name: 'Jacket 2',
    },
    {
      id: 13,
      name: 'Jacket 3',
    },
    {
      id: 14,
      name: 'Jacket 4',
    },
    {
      id: 15,
      name: 'Hoodie 1',
    },
    {
      id: 16,
      name: 'Hoodie 2',
    },
    {
      id: 17,
      name: 'Hoodie 3',
    },
    {
      id: 18,
      name: 'Hoodie 4',
    },
  ],
  max: 6,
}

const selected_items = reactive({
  left: new Set(),
  right: new Set(),
} as { left: Set<Item>; right: Set<Item> })

const userItemSelect = (item: Item) => {
  if (selected_items.left.size === items.max) return
  selected_items.left.add(item)
}
</script>

<template>
  <header>
    <ItemsBox
      class="user-items"
      :items="Array.from(selected_items.left)"
      @item-click="selected_items.left.delete($event)"
    />
    <Item
      class="selected-item"
      :item="Array.from(selected_items.right)[0]"
    />
  </header>
  <main>
    <ItemsBox
      :items="items.left"
      :selected-items="selected_items.left"
      @item-click="userItemSelect($event)"
    />
    <ItemsBox
      :items="items.right"
      :selected-items="selected_items.right"
      @item-click="selected_items.right = new Set([$event])"
    />
  </main>
</template>

<style lang="scss">
* {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
  border: 0;
  outline: 0;
  line-height: 1;
}

body {
  padding: 10px;
  height: 100vh;
}

#app {
  display: flex;
  flex-direction: column;

  &,
  main {
    height: 100%;
  }

  main,
  & > header {
    display: flex;
    justify-content: space-between;
    gap: 10px;
  }

  & > header {
    margin-bottom: 10px;

    .user-items {
      position: relative;
      width: 25%;
      grid-template-columns: repeat(2, 1fr);
      padding-bottom: 46px;
      counter-reset: user-item 0;

      &:after {
        content: 'selected: ' counter(user-item) ' / 6';
        position: absolute;
        left: 50%;
        bottom: 10px;
        transform: translateX(-50%);
        color: white;
      }

      li {
        counter-increment: user-item 1;
      }
    }

    .selected-item {
      width: 25%;
      height: unset;
      border: 10px solid grey;
    }
  }
}
</style>
