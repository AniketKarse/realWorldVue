<script setup>

const props = defineProps(['event']); //the short way

</script>

<template>
    <p>@ {{ event.time }} on {{ event.date }} </p>
    <p>{{ event.description }}</p>
</template>