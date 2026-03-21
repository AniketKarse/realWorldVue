<script setup>
import { ref, onMounted, computed } from 'vue'
import { RouterView, RouterLink, useRouter } from 'vue-router'
import EventService from '@/services/EventService.js'

const router = useRouter()

const props = defineProps({
    id: {
        required: true,
    }
})
const id = computed(() => props.id);
const event = ref(null)
// const props = defineProps(['id']); //the short way

onMounted(() => {
    EventService.getEvent(id.value)
        .then((response) => {
            event.value = response.data
        })
        .catch((error) => {
            if (error.response && error.response.status == 404) {
                router.push({
                    name: '404Resource',
                    params: { resource: 'event' }
                })
            }
            else {
                router.push({ name: 'NetworkError' })
            }
        })
})

</script>

<template>

    <div v-if="event">
        <div class="event-card">
            <h2>{{ event.title }}</h2>
            <div id="nav">
                <RouterLink :to="{ name: 'EventDetails' }">Details</RouterLink> |
                <RouterLink :to="{ name: 'EventRegister' }">Register</RouterLink> |
                <RouterLink :to="{ name: 'EventEdit' }">Edit</RouterLink>
            </div>
            <RouterView :event="event" />
        </div>
    </div>

</template>

<style>
.event-card {
    text-decoration: none;
}
</style>