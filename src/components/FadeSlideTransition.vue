<template>
  <Transition name="fadeSLide" mode="out-in">
    <slot></slot>
  </Transition>
</template>


<script setup>

</script>


<style lang="scss">
  .fadeSLide-enter-from {
    opacity: 0;
    transform: translateY(-10px);
  }
  .fadeSLide-leave-to {
    transform: translateY(-10px);
    opacity: 0;
  }
</style>