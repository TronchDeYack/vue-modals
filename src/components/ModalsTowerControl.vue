<script setup>
import { ref } from 'vue'
import Modal from './Modal.vue'
import MyButton from './MyButton.vue'

const openModal = ref(false)
const openModal2 = ref(false)
const openModal3 = ref(false)
</script>

<template>
  <div class="p-8 rounded-lg bg-white border border-white flex flex-wrap space-x-4">
    <div>
      <MyButton @click="openModal = true">
        With default text
      </MyButton>
      <Modal v-model:shown="openModal" text="Hello from the modal !" title="A title"/>
    </div>

    <div>
      <MyButton type="alert" @click="openModal2 = true">
        With custom text
      </MyButton>
      <Modal v-model:shown="openModal2">
        <template #header>
          <h3 class="text-2xl text-red-800 font-extrabold">Enter your information</h3>
        </template>
        <template #content>
          <div>
            <h3 class="font-medium mb-1">Please enter your name : </h3>
            <input class="border border-gray-400 rounded-md px-2 py-1 w-full"/>
          </div>
        </template>
        <template #actions>
          <MyButton type="confirm" @click="openModal2 = false" />
        </template>
      </Modal>
    </div>

    <div>
      <MyButton type="confirm" @click="openModal3 = true">
        With search bar
      </MyButton>
      <Modal v-model:shown="openModal3" with-search>
        <template #content="{ search }">
          You are looking for {{ search }}
        </template>
      </Modal>
    </div>
  </div>
</template>
