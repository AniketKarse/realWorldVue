<script setup>
import { useRouter } from 'vue-router';

const router = useRouter()

const props = defineProps(['event']); //the short way

const register = () => {
    router.push({
        name: 'EventDetails'
    })
}
</script>

<template>
    <p>Register for the event</p>
    <button @click="register">Register me!</button>
</template>