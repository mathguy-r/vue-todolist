<script setup lang="ts">
import { Heading } from 'flowbite-vue'
import TaskSnippet from './components/TaskSnippet.vue';
import { computed, ref } from 'vue';
import Task from './types/Task.ts';
import ModalForm from './components/ModalForm.vue';


const taskList = ref<Task[]>([
  { id: 0, title: "This is task #1", description: "Lorem ipsum dolor sit amet." },
  { id: 1, title: "This is task #2", description: "Lorem ipsum dolor sit amet." },
  { id: 2, title: "This is task #3", description: "Lorem ipsum dolor sit amet." },
]);

const newTitle = ref('');
const newDescription = ref('');

const addTaskSubmit = () => {
  const newId = Math.max(...taskList.value.map((obj) => obj.id))
  taskList.value.push({
    id: newId,
    title: newTitle.value,
    description: newDescription.value
  })
  newTitle.value = ''
  newDescription.value = ''
  addTaskOpen.value = false
};

const searchKeyWord = ref('');
const filteredTaskList = computed(() => {
  return taskList.value.filter(obj => obj.title.includes(searchKeyWord.value))
});

const deleteTask = (task: Task) => {
  taskList.value = taskList.value.filter(x => x != task)
};

const addTaskOpen = ref(false);
const openAddTaskForm = () => {
  addTaskOpen.value = true
};

</script>

<template>
  <div class="w-screen h-screen overflow-y-scroll bg-gray-50 dark:bg-gray-900">
    <section class="max-h-max flex items-center py-8">
      <div class="max-w-screen-md px-4 mx-auto md:px-8 w-full">
        <!-- Start coding here -->
        <div class="relative bg-white shadow-md dark:bg-gray-800 sm:rounded-lg">
          <Heading tag="h1" color="text-gray-900 dark:text-white" class="inline-flex justify-center p-8 font-semibold">
            Vue Todo List App
          </Heading>
          <div class="flex flex-col items-center justify-between p-4 space-y-3 md:flex-row md:space-y-0 md:space-x-4">
            <div class="w-full md:w-1/2">
              <form class="flex items-center">
                <label for="simple-search" class="sr-only">Search</label>
                <div class="relative w-full">
                  <div class="absolute inset-y-0 left-0 flex items-center pl-3 pointer-events-none">
                    <svg aria-hidden="true" class="w-5 h-5 text-gray-500 dark:text-gray-400" fill="currentColor"
                      viewbox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
                      <path fill-rule="evenodd"
                        d="M8 4a4 4 0 100 8 4 4 0 000-8zM2 8a6 6 0 1110.89 3.476l4.817 4.817a1 1 0 01-1.414 1.414l-4.816-4.816A6 6 0 012 8z"
                        clip-rule="evenodd" />
                    </svg>
                  </div>
                  <input type="text" id="simple-search" v-model="searchKeyWord"
                    class="block w-full p-2 pl-10 text-sm text-gray-900 border border-gray-300 rounded-lg bg-gray-50 focus:ring-purple-500 focus:border-purple-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-purple-500 dark:focus:border-purple-500"
                    placeholder="Search" required>
                </div>
              </form>
            </div>
            <div
              class="flex flex-col items-stretch justify-end flex-shrink-0 w-full space-y-2 md:w-auto md:flex-row md:space-y-0 md:items-center md:space-x-3">
              <button type="button" @click="openAddTaskForm"
                class="flex items-center justify-center px-4 py-2 text-sm font-medium text-white rounded-lg bg-purple-700 hover:bg-purple-800 focus:ring-2 focus:ring-purple-300 dark:bg-purple-600 dark:hover:bg-purple-700 focus:outline-none dark:focus:ring-purple-800">
                <i class="fa-solid fa-plus pe-2"></i>
                Add Task
              </button>
            </div>
          </div>
        </div>
        <!-- form modal -->
        <Teleport to=".form-modal" v-if="addTaskOpen">
          <ModalForm :isShowModal="addTaskOpen" v-model:new-title="newTitle" v-model:new-description="newDescription"
            @taskCreate="addTaskSubmit" @closeForm="addTaskOpen = false" />
        </Teleport>
        <!-- hr section -->
        <hr class="h-px my-8 bg-gray-200 border-0 dark:bg-gray-700">
        <!-- list section -->
        <!-- Start coding here -->
        <div v-if="filteredTaskList.length">
          <TaskSnippet v-for="task in filteredTaskList" :task="task" :key="task.id" @delete="deleteTask(task)" />
        </div>
        <div v-else>
          <p class="text-gray-500 dark:text-gray-400 italic"> Nothing matched !!!</p>
        </div>
        <!-- another  -->

      </div>
    </section>

  </div>
</template>

<style scoped></style>