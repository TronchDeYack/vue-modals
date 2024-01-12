<script setup>
defineProps({
  type: {
    type: String,
    default: 'submit',
    validator: (t) => ['alert', 'confirm', 'cancel', 'submit'].includes(t),
  }
})

defineEmits(['click'])
</script>

<template>
  <button 
    class="rounded-lg text-white font-semibold px-4 py-2" 
    :class="{
      'bg-blue-700': type === 'submit',
      'bg-green-700': type === 'confirm',
      'bg-red-700': type === 'alert',
      'bg-gray-500': type === 'cancel',
    }"
    @click="$emit('click')"
  >
    <slot>Submit</slot>
  </button>
</template>