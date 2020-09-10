<template>
  <div class="fi-fileinput">
    <label class="fi-label" >{{label}}</label>
    <label class="fi-select">
      <div class="fi-select-button">
        <span v-if="value" class="fi-selected-name fi-fileinput-text">
          <inline-svg
              :src="fileIcon"
              width="20"
              height="20"
              fill="black"
              aria-label="attachFile"
          ></inline-svg>
          Selected file: {{value.name}}
        </span>
        <span v-else class="fi-fileinput-text">
          <inline-svg
              :src="fileIcon"
              width="20"
              height="20"
              fill="black"
              aria-label="attachFile"
          ></inline-svg>
          Select a file</span>
      </div>
      <input
        type="file"
        @change="handleFileChange"
        class="fi-input"
        accept="image/png, image/jpeg, image/png, image/gif"
        />
    </label>
    <span class="fi-border"></span>
  </div>
</template>

<script>
export default {
  name: 'FileInput',
  data () {
    return {
      fileIcon: require('../assets/attach.svg')
    }
  },
  props: {
    value: File,
    label: String
  },
  methods: {
    handleFileChange (e) {
      this.$emit('input', e.target.files[0])
    }
  }
}
</script>

<style scoped>
.fi-fileinput {
  width: 90%;
  margin-left: 15px;
  margin-top: 0;
  position: relative;
  border-bottom: 1px solid #ccc;
}
.fi-fileinput-text {
  font-size: 20px;
}
.fi-selected-name {
    margin-top: 38px;
}
.fi-label {
    display: block;
    font-weight: 500;
    color: black;
    font-size: 12px;
    text-align: left;
    margin-bottom: 10px;
}
.fi-select > .fi-select-button {
  color: black;
  background-color: white;
  text-align: left;
  font-weight: bold;
  font-size: 14px;
  margin-top: 14px;
}

.fi-select > input[type="file"] {
  display: none;
}
.fi-input ~ .fi-border {
  position: absolute;
  bottom: 2px;
  left: 0;
  width: 0;
  height: 0.1px;
  background-color: black;
  -webkit-transition: width 250ms ease-in-out;
  transition: width 250ms ease-in-out;
}
.fi-input:focus ~ .fi-border {
  width: 100%;
  -webkit-transition: width 250ms ease-in-out;
  transition: width 250ms ease-in-out;
}
</style>
