<script setup>
import { ref } from 'vue';

defineProps({
  shown: {
    type: Boolean,
    required: true,
  },
  title: {
    type: String,
    default: null,
  },
  text: {
    type: String,
    default: null,
  },
  withSearch: {
    type: Boolean,
    default: false,
  }
})

const searchText = ref()

defineEmits(['update:shown'])
</script>

<template>
  <Teleport to="#modal">
    <Transition name="modal">
      <div 
        v-if="shown" 
        class="fixed z-50 top-0 left-0 w-full h-full bg-opacity-50 bg-black flex transition-all"
      >
        <div class="bg-white rounded-2xl p-4 text-black w-80 shadow-sm m-auto">
          <slot name="header">
            <h2 class="font-semibold text-lg">{{ title }}</h2>
          </slot>

          <input v-if="withSearch" v-model="searchText" class="border border-gray-400 rounded-md px-2 py-1 w-full"/>

          <slot name="content" :search="searchText">
            <p class="font-medium text-gray-800">{{ text }}</p>
          </slot>
          
          <div class="mt-4 flex justify-end space-x-2">
            <button 
              class="rounded-lg bg-gray-500 text-white font-semibold px-4 py-2"
              @click="$emit('update:shown', false)"
            >
              Close
            </button>
            <slot name="actions" />
          </div>
        </div>
      </div>
    </Transition>
  </Teleport>
</template>

<style lang="postcss" scoped>
.modal-enter-from,
.modal-leave-to {
  opacity: 0;
}

.modal-enter-from,
.modal-leave-to {
  transform: scale(1.1);
}
</style>
