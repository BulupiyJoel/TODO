<script setup>
defineProps({
      className: {
            type: String,
            required: true,
      },
      label: {
            type: String,
            required: true,
      },

})

</script>
<template>
      <button :class=className>
            <slot></slot> {{ label }}
      </button>
</template>