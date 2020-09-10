<template>
  <div class="sel">
    <label class="sel-label">
      {{label}}{{required ? '* ' : ''}}<span style="color:red">{{errorInfo}}</span>
    </label>
    <div class="sel-content">
      <input class="sr-only radio-toggle" id="birth-toggle" name="birthdate" type="radio">
      <label class="select-toggle sel-content-label" for="birth-toggle">
        <b class="sh-indicator"></b>
        <i class="sr-only">select</i>
      </label>
      <span class="select">
        <input class="sr-only" id="birth1900" name="birthdate" type="radio">
        <label for="birth1900" class="sel-content-label">text 1</label>
        <input class="sr-only" id="birth1901" name="birthdate" type="radio">
        <label for="birth1901" class="sel-content-label">text 2</label>
        <input class="sr-only" id="birth1902" name="birthdate" type="radio">
        <label for="birth1902" class="sel-content-label">text 3</label>
      </span>
    </div>
    <span class="sel-border"></span>
  </div>
</template>

<script>
export default {
  name: 'Select',
  data () {
    return {
      errorInfo: ''
    }
  },
  props: {
    name: {
      type: String,
      required: true,
      default: ''
    },
    label: {
      type: String,
      required: true,
      default: ''
    },
    required: {
      type: Boolean,
      required: false,
      default: false
    },
    readOnly: {
      type: Boolean,
      required: false,
      default: false
    }

  }
}
</script>

<style scoped>
.sel-content {
  position: relative;
}
.sel-label {
  display: block;
  font-size: 11px;
  text-align: left;
  margin-bottom: 10px;
  font-weight: bold;
}
/* Works like the <option/> tag */
.sel-content-label {
  background: #fff;
  color: #666;
  display: block;
  padding: 0 0.5em;
}
/* Works like the <select/> tag */
.select {
  background: #fff;
  /* border: solid 0 #999; */
  z-index: 1;
}
.select-toggle,
.select,
.select label {
  left: 0;
  text-align: left;
  /* line-height: 1.8em; */
  min-height: 2em;
  position: absolute;
  right: 0;
  top: 0;
}
/* Toggle for the select box opening and closing */
.select-toggle,
.select-toggle:hover {
  background: none;
  text-align: right;
  z-index: 2;
}
/* For keyboard navigation: highlights the select box, when the toggle radio button is in focus */
.radio-toggle:focus ~ .select {
  outline: none;
}
/* Select term toggle (open) */
.radio-toggle:checked + .select-toggle {
  left: auto;
}
/* The downward pointing triangle inside the select toggle */
.sh-indicator {
  border-left: 0.3em solid transparent;
  border-right: 0.3em solid transparent;
  border-top: 0.6em solid black;
  display: inline-block;
  line-height: 0;
}

.sel-content-label:hover,
.sel-content-label:focus {
  cursor: pointer;
}
/* This shuffles the sorting order of the stack of "option" tags, so that either the first, or the selected is on top. */
.select label:first-of-type,
.select input:checked + label {
  z-index: 1;
}
/* Once the toggle has been triggered, the fake option tags stop stacking on top of each other, and stack vertically. */
.radio-toggle:checked ~ .select label {
  position: static;
}

/* Visually hidden only */
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  margin: -1px;
  padding: 5px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  border: 0;
}

.sel-border {
  border-bottom: 0.1px solid #000;
  z-index:4;
}

.radio-toggle ~ .sel-border {
  position: absolute;
  bottom: 2px;
  left: 0;
  width: 0;
  height: 0.1px;
  background-color: black;
  -webkit-transition: width 250ms ease-in-out;
  transition: width 250ms ease-in-out;
}
.radio-toggle:focus ~ .sel-border {
  width: 100%;
  -webkit-transition: width 250ms ease-in-out;
  transition: width 250ms ease-in-out;
}
</style>
