<script setup>
defineProps({
  title: String,
  type: {
    type: String, // 'is-dark', 'is-primary', 'is-rounded', etc.
    default: 'is-dark'
  },
  withTitle: {
    type: Boolean,
    default: true
  }
});
</script>

<template>
  <div :class="['nes-container', type, { 'with-title': withTitle }]">
    <p v-if="withTitle && title" class="title">{{ title }}</p>
    <slot></slot>
  </div>
</template>

<style scoped>
.nes-container {
  max-width: 600px;
  background-color: white; /* Default background */
  color: black;
  margin: 10px;
  position: relative;
}

.nes-container.is-dark {
  background-color: #212529;
  color: white;
}
</style>
