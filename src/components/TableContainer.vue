<template>
  <div class="flex-container">
    <slot />
  </div>
</template>

<script>
export default {
  name: 'TableContainer'
}
</script>

<style scoped>
.flex-container {
  display: flex;
  flex-wrap: wrap;
}
</style>
