<template>
  <label>
    <input type="checkbox" @change="onChange" v-model="model" />
    {{ label }}
  </label>
</template>

<script setup>
const props = defineProps({
  label: String,
});

const model = defineModel();

const onChange = (event) => {
  if (event.currentTarget.checked) {
    emits("check", event.currentTarget);
  } else {
    emits("uncheck", event.currentTarget);
  }
};

const emits = defineEmits(["check", "uncheck"]);

console.log(props.label);
</script>
