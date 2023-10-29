<script lang="ts" setup>
const emit = defineEmits(['search']);

const search = (event: Event) => {
   const target = event.target as HTMLInputElement;
    emit('search', target.value)
};
</script>

<template>
    <form class="flex items-center px-4 py-3">
        <label for="search-input" class="sr-only ">Search</label>
        <div class="relative w-full ">
            <input id="search-input" type="search" @input="search" placeholder="Search" name="search" class="px-4 py-2 text-gray-900 border border-gray-300 rounded-md bg-gray-50">
        </div>
    </form>
</template>