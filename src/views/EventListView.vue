<script setup>
import { onMounted, ref, watch, computed } from 'vue';
import EventCard from '@/components/EventCard.vue';
import EventService from '@/services/EventService.js'
import { RouterLink } from 'vue-router'

const events = ref(null);

const props = defineProps(['page'])
const totalEvents = ref(0)
const fetchevents = () => {
  EventService.getEvents(2, props.page)
    .then((response) => {
      events.value = response.data
      totalEvents.value = response.headers["x-total-count"]
    })
    .catch((error) => {
      console.log(error)
    })
}

const hasNext = computed(() => {
  const totalPages = Math.ceil(totalEvents.value / 2)
  return props.page < totalPages
})


onMounted(() => {
  fetchevents()
})

watch(
  () => props.page,
  () => {
    events.value = null
    fetchevents()
  }
)
</script>

<template>
  <div class="events">
    <h1>Events for good</h1>
    <EventCard v-for="event in events" :key="event.id" :event="event" />
    <div class="pagination">
      <RouterLink id="page-prev" :to="{ name: 'event-list', query: { page: page - 1 } }" rel="prev" v-if="page != 1">
        &#60; Previous</RouterLink>

      <RouterLink id="page-next" :to="{ name: 'event-list', query: { page: page + 1 } }" rel="next" v-if="hasNext">Next
        &#62;
      </RouterLink>
    </div>
  </div>
</template>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.pagination {
  display: flex;
  width: 290px;
}

.pagination a {
  flex: 1;
  text-decoration: none;
  color: #2c3e50;
}

#page-prev {
  text-align: left;
}

#page-next {
  text-align: right;
}
</style>