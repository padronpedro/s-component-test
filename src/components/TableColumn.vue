<template>
  <div class="flex-col">
    <slot />
  </div>
</template>

<script>
export default {
  name: 'TableColumn'
}
</script>

<style scoped>
.flex-col {
  flex: 25%;
  margin: 10px;
  text-align: center;
}

@media screen and (max-width: 992px) {
  .flex-col {
    flex: 50%;
  }
}

@media screen and (max-width: 600px) {
  .flex-col {
    flex-direction: column;
  }
}
</style>
