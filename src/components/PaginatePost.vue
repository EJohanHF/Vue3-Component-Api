<script setup>
defineProps(["inicio", "fin", "maxLengthpost"]);

const emit = defineEmits(["nextPage", "previusPage"]);
</script>

<template>
  <div class="btn-group" role="group" aria-label="Basic example">
    <button
      :disabled="inicio === 0"
      @click="emit('previusPage')"
      type="button"
      class="btn btn-outline-primary"
    >
      Previus
    </button>
    <button
      :disabled="fin >= maxLengthpost"
      @click="emit('nextPage')"
      type="button"
      class="btn btn-outline-primary"
    >
      Next
    </button>
  </div>
</template>
