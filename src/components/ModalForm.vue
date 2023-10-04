<script setup lang="ts">
import { Modal } from 'flowbite-vue'

defineProps<{
    isShowModal: boolean,
    newTitle: String,
    newDescription: String,
}>();

defineEmits(['update:newTitle', 'update:newDescription', 'closeForm','taskCreate'])

</script>

<template>
    <Modal v-if="isShowModal" @close="$emit('closeForm')">
        <template #header>
            <div class="flex items-center text-lg text-gray-900 dark:text-white">
                Create New Task
            </div>
        </template>
        <template #body>
            <form>
                <div class="mb-6">
                    <label for="task-title" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Task
                        Title</label>
                    <input type="text" id="task-title" 
                        class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-purple-500 focus:border-purple-500 block w-full p-2.5 dark:bg-gray-800 dark:border-gray-700 dark:placeholder-gray-400 dark:text-white dark:focus:ring-purple-500 dark:focus:border-purple-500"
                        placeholder="Task#1" required autofocus :value="newTitle" @input="$emit('update:newTitle', ($event.target as HTMLInputElement).value)">
                </div>
                <div class="mb-6">
                    <label for="task-description" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Task
                        Description</label>
                    <input type="text" id="task-description" :value="newDescription" @input="$emit('update:newDescription', ($event.target as HTMLInputElement).value)"
                        class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-purple-500 focus:border-purple-500 block w-full p-2.5 dark:bg-gray-800 dark:border-gray-700 dark:placeholder-gray-400 dark:text-white dark:focus:ring-purple-500 dark:focus:border-purple-500"
                        placeholder="Some description text ...">
                </div>
                <button type="submit" @click="$emit('taskCreate')"
                    class="text-white bg-purple-700 hover:bg-purple-800 focus:ring-4 focus:outline-none focus:ring-purple-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center dark:bg-purple-600 dark:hover:bg-purple-700 dark:focus:ring-purple-800">
                    Submit
                </button>
            </form>
        </template>
    </Modal>
</template>

<style scoped></style>

