<template>
  <div>
    <td-button color="primary">
      {{ testText }}
    </td-button>
  </div>
</template>
<script setup>
definePageMeta({
  layout: "app",
});

const testText = "kozderka.dev";
</script>
