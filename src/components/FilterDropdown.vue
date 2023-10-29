<script lang="ts" setup>
import type { Task } from '@/Task';
import { ref, type PropType, computed } from 'vue';

const show = ref(false);

const props = defineProps({
    items: {
        type: Array as PropType<Task[]>,
        required: true
    }
});

const statuses = computed(() => [...new Set(props.items.map(item => item.status))]);

const emit = defineEmits(['filter']);

const filter = (event: Event) => {
    const target = event.target as HTMLInputElement;
    emit('filter', target.value);
};
</script>

<template>
    <div class="relative flex items-center w-full px-4">
        <button  @click="show = !show" class="flex items-center justify-center w-full px-4 py-2 text-sm font-medium text-gray-900 border-2 rounded-lg hover:bg-gray-100">
            Filter
        </button>

        <div v-if="show" class="absolute right-0 z-10 w-48 p-3 bg-white rounded-lg shadow top-12">
            <h6 class="mb-3 text-sm font-medium text-gray-900 ">Status</h6>
            <ul class="space-y-2 text-sm">
                <li v-for="status in statuses" :key="status">
                    <input :id="`filter_option_${status}`" @change="filter" type="checkbox" :value="status" class="w-4 h-4 bg-gray-100 border-gray-300 rounded">
                    <label :for="`filter_option_${status}`" class="ml-2 text-sm font-medium text-gray-900 "> {{ status }}</label>
                </li>
            </ul>
        </div>
    </div>
</template>