<script setup lang="ts">
import { ref } from 'vue';
import Task from '../types/Task';

const props = defineProps<{
    task:Task
}>()

const taskDone = ref(false);
const taskCompleted = () =>{
    taskDone.value = true
};

</script>

<template>
    <div class="relative overflow-hidden bg-white shadow-md dark:bg-gray-800 sm:rounded-lg my-4">
        <div class="flex-row items-center justify-between p-4 space-y-3 sm:flex sm:space-y-0 sm:space-x-4">
            <div>
                <h5 class="mr-3 font-semibold dark:text-white" :class="{'line-through italic':taskDone}">{{props.task.title}}</h5>
                <p class="text-gray-500 dark:text-gray-400" :class="{'line-through italic':taskDone}">{{props.task.description}}</p>
            </div>
            <div class="flex w-auto flex-row space-y-0 items-center space-x-6">
                <button type="button" v-show="!taskDone" @click="taskCompleted"
                    class="flex items-center justify-center px-4 py-2 text-sm font-medium text-white rounded-lg bg-emerald-700 hover:bg-emerald-800 focus:ring-2 focus:ring-emerald-300 dark:bg-emerald-600 dark:hover:bg-emerald-700 focus:outline-none dark:focus:ring-emerald-800">
                    <i class="fa-solid fa-check"></i>
                </button>
                <button type="button" @click="$emit('delete')"
                    class="flex items-center justify-center px-4 py-2 text-sm font-medium text-white rounded-lg bg-red-700 hover:bg-red-800 focus:ring-2 focus:ring-red-300 dark:bg-red-600 dark:hover:bg-red-700 focus:outline-none dark:focus:ring-red-800">
                    <i class="fa-solid fa-trash"></i>
                </button>
            </div>
        </div>
    </div>
</template>

<style scoped></style>