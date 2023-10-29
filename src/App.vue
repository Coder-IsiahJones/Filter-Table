<script setup lang="ts">
import { ref } from 'vue';
import DataTable from './components/DataTable.vue'
import type { Task } from './Task';

const items = ref<Task[]>([
  {
    id: 1,
    user: {
      name: 'John Doe',
    },
    status: 'open',
    title: 'Update the documentation',
    due_at: '2024-11-10',
  },
  {
    id: 2,
    user: {
      name: 'Jane Doe',
    },
    status: 'closed',
    title: 'Update the documentation',
    due_at: '2020-10-03',
  },
  {
    id: 3,
    user: {
      name: 'John Doe',
    },
    status: 'pending',
    title: 'Update the documentation',
    due_at: '2020-10-03',
  },
  {
    id: 4,
    user: {
      name: 'Alice Smith',
    },
    status: 'open',
    title: 'Review code changes',
    due_at: '2024-11-15',
  },
  {
    id: 5,
    user: {
      name: 'Bob Johnson',
    },
    status: 'closed',
    title: 'Bug fixes',
    due_at: '2021-05-20',
  },
  // Add more task data for testing
  {
    id: 6,
    user: {
      name: 'Eve Johnson',
    },
    status: 'pending',
    title: 'Write documentation',
    due_at: new Date().toISOString().slice(0, 10)
  },
  {
    id: 7,
    user: {
      name: 'Grace Williams',
    },
    status: 'open',
    title: 'Feature development',
    due_at: '2023-09-08',
  },
  {
    id: 8,
    user: {
      name: 'David Brown',
    },
    status: 'closed',
    title: 'UI improvements',
    due_at: '2022-12-12',
  },
  {
    id: 9,
    user: {
      name: 'Emma Wilson',
    },
    status: 'pending',
    title: 'Testing and QA',
    due_at: '2023-02-25',
  },
  {
    id: 10,
    user: {
      name: 'Frank Miller',
    },
    status: 'open',
    title: 'Backend enhancements',
    due_at: '2023-07-31',
  },
  {
    id: 11,
    user: {
      name: 'Hannah Davis',
    },
    status: 'closed',
    title: 'Database optimization',
    due_at: '2022-10-05',
  },
  {
    id: 12,
    user: {
      name: 'Ian White',
    },
    status: 'pending',
    title: 'Code review',
    due_at: '2023-04-17',
  },
  {
    id: 13,
    user: {
      name: 'Julia Clark',
    },
    status: 'open',
    title: 'Frontend redesign',
    due_at: '2024-02-14',
  },
  {
    id: 14,
    user: {
      name: 'Kevin Lee',
    },
    status: 'closed',
    title: 'Deployment planning',
    due_at: '2022-07-19',
  },
  {
    id: 15,
    user: {
      name: 'Linda Harris',
    },
    status: 'pending',
    title: 'Infrastructure setup',
    due_at: '2023-06-29',
  },
  {
    id: 16,
    user: {
      name: 'Mike Robinson',
    },
    status: 'open',
    title: 'Client meetings',
    due_at: '2024-09-23',
  },
  {
    id: 17,
    user: {
      name: 'Nina Garcia',
    },
    status: 'closed',
    title: 'Data analysis',
    due_at: '2022-08-08',
  },
  {
    id: 18,
    user: {
      name: 'Oliver Taylor',
    },
    status: 'pending',
    title: 'Project kickoff',
    due_at: '2023-03-12',
  },
  {
    id: 19,
    user: {
      name: 'Paula Anderson',
    },
    status: 'open',
    title: 'Documentation review',
    due_at: '2024-01-07',
  },
  {
    id: 20,
    user: {
      name: 'Quincy Hall',
    },
    status: 'closed',
    title: 'Testing automation',
    due_at: '2022-09-14',
  },
  {
    id: 21,
    user: {
      name: 'Rachel King',
    },
    status: 'pending',
    title: 'Feature planning',
    due_at: '2023-05-18',
  },
  {
    id: 22,
    user: {
      name: 'Samuel Martinez',
    },
    status: 'open',
    title: 'Code refactoring',
    due_at: '2024-04-30',
  },
  {
    id: 23,
    user: {
      name: 'Tina Walker',
    },
    status: 'closed',
    title: 'Performance tuning',
    due_at: '2022-11-25',
  },
  {
    id: 24,
    user: {
      name: 'Ulysses Green',
    },
    status: 'pending',
    title: 'Database migration',
    due_at: '2023-08-06',
  },
  {
    id: 25,
    user: {
      name: 'Vera Adams',
    },
    status: 'open',
    title: 'Security audit',
    due_at: '2024-06-12',
  },
]);

const addTaskWithTodaysDate = () => {
  items.value.push({
    id: 26,
    user: {
      name: 'William Turner',
    },
    status: 'pending',
    title: 'New feature development',
    due_at: new Date().toISOString().slice(0, 10)
  });
};

addTaskWithTodaysDate();
</script>

<template>
  <div class="min-h-screen p-8 bg-gray-100">
    <DataTable :items="items" />
  </div>
</template>