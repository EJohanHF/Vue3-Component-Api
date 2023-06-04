<script setup>
    import { ref } from 'vue';

    const counter = ref(0)
    const incremen = () => counter.value++
</script>

<template>
    <button @click="incremen">counter - {{ counter }}</button>
</template>