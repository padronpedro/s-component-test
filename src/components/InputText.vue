<template>
  <div class="it-ext">
    <div v-if="leftIcon" class="it-icon">
      <div
        class="it-border-icon"
        @click.prevent="$emit('left-icon-click')"
        >
        <inline-svg
            :src="leftIcon"
            width="20"
            height="20"
            fill="black"
            :aria-label="'leftIcon_'+label"
        ></inline-svg>
      </div>
    </div>
    <div class="it-element">
      <label class="it-label">
        {{label}}{{required ? '* ' : ''}}<span style="color:red">{{errorInfo}}</span>
      </label>
      <input
        :type="inputType"
        :class="{'it-input': true, 'it-input-date': (inputType==='date')}"
        v-if="inputType!=='number'"
        autocomplete="new-password"
        @input="$emit('input',$event.target.value)"
        @blur="checkLabel($event)"
        :readonly="readOnly"
        :required="required"
        name="name"
        :value="$attrs.value">
      <input
        :type="inputType"
        class="it-input"
        :step="step"
        v-if="inputType==='number'"
        autocomplete="new-password"
        @input="$emit('input',$event.target.value)"
        @blur="checkLabel($event)"
        :readonly="readOnly"
        :required="required"
        name="name"
        :value="$attrs.value">
      <span :class="{'it-border': (inputType!=='date'),'it-border-date': (inputType==='date')}"/>
    </div>
    <div
      v-if="rightIcon"
      class="it-icon"
      @click.prevent="$emit('right-icon-click')"
    >
      <inline-svg
          :src="rightIcon"
          width="20"
          height="20"
          fill="black"
          :aria-label="'rightIcon_'+label"
      ></inline-svg>
    </div>
  </div>
</template>

<script>
export default {
  name: 'InputText',
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
    inputType: {
      type: String,
      required: true,
      default: 'text'
    },
    label: {
      type: String,
      required: true,
      default: ''
    },
    step: {
      type: Number,
      required: false,
      default: 1
    },
    leftIcon: {
      type: String,
      required: false,
      default: ''
    },
    rightIcon: {
      type: String,
      required: false,
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
  },
  methods: {
    checkLabel (e) {
      let errorFound = false
      if (this.inputType === 'number') {
        if (Number(e.target.value) > 99999.99) {
          this.errorInfo = '  Max value is 99999.99'
          this.$emit('reportError', this.name, true)
          errorFound = true
        } else {
          this.errorInfo = ''
          this.$emit('reportError', this.name, false)
        }
      }
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
.it-ext {
  margin: 10px;
  display: flex;
  justify-content: start;
  position: relative;
}
.it-element{
  flex-grow: 10;
}
.it-icon {
  flex-grow: 0.1;
  margin-top: 20px;
}
.it-icon:hover{
  cursor: pointer;
}
.it-label {
  display: block;
  font-size: 11px;
  text-align: left;
  margin-bottom: 10px;
  font-weight: bold;
}
.it-input {
  border: 0;
  width: 96%;
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  border-bottom: 0.1px solid lightgray;
  font-size: 20px;
  font-weight: bold;
}
.it-input {
  padding-bottom: 5px;
}
.it-input-date {
  padding-bottom: 2px;
  font-size: 20px;
}
.it-border, .it-border-date {
  border-bottom: 0.1px solid #000;
}
.it-input:focus {
  outline: none;
}
.it-input ~ .it-border {
  position: absolute;
  bottom: 2px;
  left: 0;
  width: 0;
  height: 0.1px;
  background-color: black;
  -webkit-transition: width 250ms ease-in-out;
  transition: width 250ms ease-in-out;
}
.it-input:focus ~ .it-border {
  width: 100%;
  -webkit-transition: width 250ms ease-in-out;
  transition: width 250ms ease-in-out;
}
.it-input ~ .it-border-date {
  position: absolute;
  bottom: 2px;
  left: 0;
  width: 0;
  height: 0.1px;
  background-color: black;
  -webkit-transition: width 250ms ease-in-out;
  transition: width 250ms ease-in-out;
}
.it-input:focus ~ .it-border-date {
  width: 100%;
  -webkit-transition: width 250ms ease-in-out;
  transition: width 250ms ease-in-out;
}

</style>
