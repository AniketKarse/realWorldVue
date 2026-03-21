<script setup>
import { ref, onMounted } from 'vue'
import EventService from '@/services/EventService.js'
const props = defineProps({
    id: {
        required: true,
    }
})
const event = ref(null)
// const props = defineProps(['id']); //the short way

onMounted(() => {
    EventService.getEvent(props.id)
        .then((response) => {
            event.value = response.data
        })
        .catch((error) => {
            console.log(error)
        })
})

</script>

<template>

    <div v-if="event">
        <div class="event-card">
            <h2>{{ event.title }}</h2>
            <span>@ {{ event.time }} on {{ event.date }} </span>
            <p>{{ event.description }}</p>
        </div>
    </div>

</template>

<style>
.event-card {
    text-decoration: none;
}
</style>