<template>
  <div>
    <button class="sbutton" @click="callAction">
      <slot />
    </button>
  </div>
</template>

<script>
export default {
  data () {
    return {

    }
  },
  methods: {
    callAction () {
      this.$emit('clickAction')
    }
  }
}
</script>

<style scoped>
.sbutton {
  appearance: none;
  border: none;
  background-color: #000;
  padding: 16px 32px;
  margin-left: 10px;
  color: #fff;
  cursor: pointer;
  width: 100%;
}

.sbutton:hover, .sbutton:active {
  background-color: #333;
}
</style>
