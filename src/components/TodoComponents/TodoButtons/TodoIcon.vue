<script setup>
defineProps({

      iconClass: {
            String,
            required: true
      }
})
</script>

<template>
      <i :class="iconClass"></i>
</template>