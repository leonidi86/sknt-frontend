<template>
<div>
  <h1 class="text-xl mb-2">Начало выходного дня (по-порядку)</h1>
  <ul class="flex flex-col items-start pl-2">
    <li
      v-for="(e, i) in preparedList"
      :key="i"
      class="flex items-center gap-1"
      :style="{ color: e.color }"
    >
      <button
        class="text-red-500"
        title="Remove"
        :data-index="i"
        @click.prevent="removeItem(i)"
      >
        <i-ic-baseline-delete-outline />
      </button>
      #{{ i + 1 }} {{ e.title }}
    </li>
  </ul>
</div>
</template>

<script setup lang="ts">
import { computed, ref } from 'vue';

interface Entity {
title: string;
color?: string;
index: number;
enabled: boolean;
}

// Этот список изменять запрещено
const list = ref<Entity[]>([
{
  title: 'позавтракать',
  color: 'red',
  index: 4,
  enabled: true,
},
{
  title: 'пойти гулять',
  color: 'green',
  index: 6,
  enabled: true,
},
{
  title: 'сходить в туалет',
  color: 'brown',
  index: 2,
  enabled: true,
},
{
  title: 'уйти на работу',
  color: 'cyan',
  index: 5,
  enabled: false,
},
{
  title: 'проснуться',
  color: 'blue',
  index: 1,
  enabled: true,
},
{
  title: 'умыться',
  color: 'purple',
  index: 3,
  enabled: true,
},
]);

const preparedList = computed(() => {
return [...list.value]
  .filter((item) => item.enabled)
  .sort((a, b) => a.index - b.index);
});

function removeItem(index: number) {
const itemIndex = list.value.findIndex((item) => item.index === preparedList.value[index].index);
if (itemIndex !== -1) {
  list.value.splice(itemIndex, 1);
}
}
</script>
