<template>
  <div class="ta">
    <label class="ta-label">
      {{label}}{{required ? '* ' : ''}}<span style="color:red">{{errorInfo}}</span>
    </label>
    <textarea
      @input="$emit('input',$event.target.value)"
      @blur="checkLabel($event)"
      autocomplete="new-password"
      :readonly="readOnly"
      :required="required"
      name="name"
      :value="$attrs.value"
      class="ta-textarea"
      rows="5"
     >
    </textarea>
    <span class="ta-border"/>
  </div>
</template>

<script>
export default {
  name: 'TextArea',
  data () {
    return {
      errorInfo: ''
    }
  },
  props: {
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
    name: {
      type: String,
      required: true,
      default: ''
    },
    readOnly: {
      type: Boolean,
      required: false,
      default: false
    }
  },
  methods: {
    checkLabel (e) {
      let errorFound = false
      if (!errorFound) {
        if (this.required) {
          this.errorInfo = e.target.validationMessage
          console.log(e, this.errorInfo)
          if (this.errorInfo) {
            this.$emit('reportError', this.name, true)
          } else {
            this.$emit('reportError', this.name, false)
          }
        }
      }
    }
  }
}
</script>

<style scoped>
.ta {
  margin: 10px;
  justify-content: start;
  position: relative;
}
.ta-textarea {
  width: 100%;
  border: 0;
  border-bottom: 0.1px solid lightgray;
  font-size: 20px;
}
.ta-textarea:focus {
  outline: none;
}
.ta-label {
  display: block;
  font-size: 11px;
  text-align: left;
  margin-bottom: 5px;
  font-weight: bold;
}
.ta-border {
  border-bottom: 0.1px solid #000;
  bottom: 1px;
}
.ta-textarea ~ .ta-border {
  position: absolute;
  bottom: 6px;
  left: 0;
  width: 0;
  height: 0.1px;
  background-color: black;
  -webkit-transition: width 250ms ease-in-out;
  transition: width 250ms ease-in-out;
}
.ta-textarea:focus ~ .ta-border {
  width: 100%;
  -webkit-transition: width 250ms ease-in-out;
  transition: width 250ms ease-in-out;
}
</style>
