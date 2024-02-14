<script setup>
import { defineProps } from 'vue';


const props = defineProps({
  items: Array,
  columns: Array
});
</script>

<template>
  <div class="overflow-x-auto">
    <table class="table">
  <thead>
  <tr>
    <th v-for="column in props.columns" :key="column.name">
      <slot :name="`header-${column.name}`">
        {{ column.label }}
      </slot>
    </th>
    <th></th>
  </tr>
</thead>
<tbody>
  <tr v-for="item in props.items" :key="item.id">
    <td v-for="column in props.columns" :key="column.name">
      <slot :name="column.name" :item="item">
        {{ item[column.name] }}
      </slot>
    </td>
    <td>
      <slot name="actions" :id="item.guid"></slot>
    </td>
  </tr>
</tbody>
    </table>
  </div>
</template>




