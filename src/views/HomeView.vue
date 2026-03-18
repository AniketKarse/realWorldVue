<script setup lang="ts">
import { ref } from 'vue';
import EventCard from '@/components/EventCard.vue';

const events = ref([
  {
    id: 1,
    title: 'Event 1',
    description: 'Description 1',
    location: 'Location 1',
    date: '2026-01-01',
    time: '10:00',
  },
  {
    id: 2,
    title: 'Event 2',
    description: 'Description 2',
    location: 'Location 2',
    date: '2026-01-02',
    time: '10:00',
  },
  {
    id: 3,
    title: 'Event 3',
    description: 'Description 3',
    location: 'Location 3',
    date: '2026-01-03',
    time: '10:00',
  },
  {
    id: 4,
    title: 'Event 4',
    description: 'Description 4',
    location: 'Location 4',
    date: '2026-01-04',
    time: '10:00',
  },
]);
</script>

<template>
  <div class="events">
    <h1>Events for good</h1>
    <EventCard v-for="event in events" :key="event.id" :event="event" />
  </div>
</template>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>