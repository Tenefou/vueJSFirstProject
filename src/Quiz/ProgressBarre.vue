<template>
  <div class="progress">
    <div class="progress-bar" :style="{ width: remplissage + '%' }"></div>
  </div>
</template>

<script setup>
defineProps({
  remplissage: {
    type: Number,
    required: true,
    validator: (value) => value >= 0 && value <= 100,
  },
});
</script>

<style>
.progress {
  width: 100%;
  max-width: 400px;
  height: 20px;
  background-color: #ddd;
  border-radius: 10px;
  overflow: hidden;
}

.progress-bar {
  height: 100%;
  background-color: #4caf50;
  transition: width 0.3s ease-in-out;
}
</style>
