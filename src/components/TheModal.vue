<script setup>
import { defineEmits } from 'vue';

const emit = defineEmits(['close']);

const props = defineProps({
  showModal: Boolean
});
</script>

<template>
  <div class="modal" :class="{ 'modal-open': showModal }"> 
    <div class="modal-box">
      <button class="btn btn-sm btn-circle btn-ghost absolute right-2 top-2" @click="emit('close')">x</button>
      <h3 class="font-bold text-lg">
        <slot name="title">Titre de zinzin</slot>
      </h3>
      <slot></slot> 
    </div>
  </div>
</template>


