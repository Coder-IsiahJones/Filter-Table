<script lang="ts" setup>
const emit = defineEmits(['filter']);

const filter = (event: Event) => {
    emit('filter', (event.target as HTMLInputElement).value);
};
</script>

<template>
    <label class="flex items-center mr-4 flex-nowrap">
        <input type="radio" name="show" value="all" checked @change="filter">
        <span class="ml-1 whitespace-nowrap">Show all</span>
    </label>

    <label class="flex items-center mr-4 flex-nowrap">
        <input type="radio" name="show" value="today" @change="filter">
        <span class="ml-1 whitespace-nowrap">Due Today</span>
    </label>

    <label class="flex items-center mr-4 flex-nowrap">
        <input type="radio" name="show" value="past" @change="filter">
        <span class="ml-1 whitespace-nowrap">Past Due</span>
    </label>
</template>