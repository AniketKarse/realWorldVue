<script setup>
import { useRouter } from 'vue-router';
import { inject } from "vue";

const router = useRouter()
const GStore = inject('GStore')
const props = defineProps(['event']); //the short way

const register = () => {
    GStore.flashMessage = 'You are successfully registered for ' + props.event.title
    setTimeout(() => {
        GStore.flashMessage = ''
    }, 3000);
    router.push({
        name: 'EventDetails'
    })
}
</script>

<template>
    <p>Register for the event</p>
    <button @click="register">Register me!</button>
</template>