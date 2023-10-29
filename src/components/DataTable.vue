<script lang="ts" setup>
import { computed, ref, type PropType } from 'vue';
import type { Task } from '../Task';
import SearchForm from './SearchForm.vue';
import FilterDropdown from './FilterDropdown.vue';
import FilterRadio from './FilterRadio.vue';

const props = defineProps({
  items: {
    type: Array as PropType<Task[]>,
    required: true
  }
})

const searchFilter = ref('');
const radioFilter = ref('');
const checkboxFilter = ref<string[]>([]);

const handleSearch = (query: string) => {
  searchFilter.value = query;
};

const filteredItems = computed(() => {
  let items = props.items;

  const currentDate = new Date();
  const currentDateWithoutTime = new Date(currentDate.getFullYear(), currentDate.getMonth(), currentDate.getDate()); // Remove time information
  switch (radioFilter.value) {
     case 'today':
    items = items.filter(item => {
      const dueDate = new Date(item.due_at);
      const dueDateWithoutTime = new Date(dueDate.getFullYear(), dueDate.getMonth(), dueDate.getDate());
      return dueDateWithoutTime.getTime() === currentDateWithoutTime.getTime();
    });
    break;
  case 'past':
    currentDateWithoutTime.setHours(0, 0, 0, 0); // Set time to the beginning of the day
    items = items.filter(item => {
      const dueDate = new Date(item.due_at);
      const dueDateWithoutTime = new Date(dueDate.getFullYear(), dueDate.getMonth(), dueDate.getDate());
      return dueDateWithoutTime.getTime() < currentDateWithoutTime.getTime();
    });
    break;
  }

  if (checkboxFilter.value.length) { 
    items = items.filter(item => checkboxFilter.value.includes(item.status));
  }

  if (searchFilter.value !== '') { 
    items = items.filter(item =>
        item.title.includes(searchFilter.value) ||
        item.user.name.includes(searchFilter.value) ||
        item.status.includes(searchFilter.value));
  }

  return items;
});

const handleRadioFilter = (query: string) => {
  radioFilter.value = query;
};

const handleCheckboxFilter = (query: string) => {
  if (checkboxFilter.value.includes(query)) {
    return checkboxFilter.value.splice(checkboxFilter.value.indexOf(query), 1);
  }
  
  return checkboxFilter.value.push(query);
};
</script>

<template>
  <div class="relative bg-white border rounded-lg">
    <!-- Navigation -->
    <div class="flex items-center justify-between">
      <!-- Search Bar -->
      <SearchForm @search="handleSearch"/>

      <!-- Radio Buttons -->
      <div class="flex items-center justify-end text-sm font-semibold">
        <FilterRadio @filter="handleRadioFilter" />

        <!-- Search Filter -->
        <FilterDropdown :items="items" @filter="handleCheckboxFilter" />
      </div>
    </div>

    <!-- Table -->
    <table class="w-full text-sm text-left text-gray-500">
      <thead class="text-xs text-gray-700 uppercase bg-gray-50">
        <tr>
          <th class="px-4 py-3">ID</th>
          <th class="px-4 py-3">Assigned To</th>
          <th class="px-4 py-3">Status</th>
          <th class="px-4 py-3">Title</th>
          <th class="px-4 py-3">Due At</th>
          <th class="px-4 py-3">
            <span class="sr-only">Actions</span>
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in filteredItems" :key="item.id" class="border-b">
          <td class="px-4 py-3 font-medium text-gray-900"> {{ item.id }}</td>
          <td class="px-4 py-3 font-medium text-gray-900"> {{ item.user.name }}</td>
          <td class="px-4 py-3"> {{ item.status }}</td>
          <td class="px-4 py-3"> {{ item.title }}</td>
          <td class="px-4 py-3"> {{ item.due_at }}</td>
          <td class="flex items-center justify-end px-4 py-3">
            <a href="#" class="text-indigo-500 hover:underline">Details</a>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>