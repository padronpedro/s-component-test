<template>
  <div class="sel">
    <label class="sel-label">
      {{label}}{{required ? '* ' : ''}}<span style="color:red">{{errorInfo}}</span>
    </label>
    <div class="sel-container">
      <input
        readonly
        id="input"
        type="text"
        value="Dropdown"
        v-model="selectOption"
        @click.prevent="clickMain"
      >
      <span class="sel-border"></span>
    <span>
      <inline-svg
          v-if="changeDisplay === 'none'"
          :src="arrowDown"
          width="35"
          height="35"
          fill="black"
          aria-label="attachFile"
      ></inline-svg>
      <inline-svg
          v-if="changeDisplay !== 'none'"
          :src="arrowUp"
          width="35"
          height="35"
          fill="black"
          aria-label="attachFile"
      ></inline-svg>
    </span>
    </div>
    <div class="selectives" :style="{display: changeDisplay}">
      <ul>
        <li
          v-for="(oneItem, index) in items" :key="index"
          :class="{'optionItem': true, 'selected': (oneItem.id===$attrs.value)}"
          @click.prevent="clickOption(oneItem.id, oneItem.name)">
            {{oneItem.name}}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Select',
  data () {
    return {
      errorInfo: '',
      selectOption: '',
      thisDisplay: 'none',
      arrowUp: require('../assets/arrow-up.svg'),
      arrowDown: require('../assets/arrow-down.svg')
    }
  },
  computed: {
    changeDisplay () {
      return this.thisDisplay
    }
  },
  mounted () {
    if (this.$attrs.value.length > 0) {
      let aux = this.items.find(elemen => {
        return elemen.id === this.$attrs.value
      })
      if (aux) {
        this.selectOption = aux.name
      }
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
    },
    items: {
      type: Array,
      required: true
    }
  },
  methods: {
    clickMain () {
      this.thisDisplay = 'block'
    },
    clickOption (id, value) {
      this.selectOption = value
      this.thisDisplay = 'none'
      this.$emit('input', id)
    },
    closeAll () {
      this.thisDisplay = 'none'
    }
  }
}
</script>

<style scoped>
.sel{
  position: relative;
}
.sel-label {
  display: block;
  font-size: 11px;
  text-align: left;
  margin-bottom: 10px;
  font-weight: bold;
  padding-left: 10px;
}
.selectives {
  height: 0;
  position: relative;
  top: 0;
  left: -40px;
  display: none;
  z-index: 4;
}
input:hover {
  cursor: pointer;
}
input::-moz-selection {
  background: white;
  color: #000;
}
input {
  width: 94%;
  border: none;
  -webkit-appearance: none;
  padding: 5px;
  border-bottom: 0.1px solid lightgray;
  border-bottom-width: 50%;
  margin-left: 2px;
  font-weight: bold;
  font-size: 20px;
}
input:focus {
  outline: none;
}
ul {
  margin-top: 1px;
  list-style-type: none;
  text-align: left;
  position: absolute;
  width: 95%;
}
li {
  width: 100%;
  border: none;
  padding: 5px;
  font-size: 20px;
  background-color: white;
  padding-left: 25px;
}
li:hover {
  background-color: rgb(250, 250, 250);
  cursor: pointer;
}
.sel-border {
  border-bottom: 0.1px solid #000;
}
input ~ .sel-border {
  position: absolute;
  left: 0;
  width: 0;
  height: 0.1px;
  margin-left: 10px;
  background-color: black;
  -webkit-transition: width 250ms ease-in-out;
  transition: width 250ms ease-in-out;
}
input:focus ~ .sel-border {
  width: 94%;
  padding-left: 10px;
  -webkit-transition: width 250ms ease-in-out;
  transition: width 250ms ease-in-out;
}
.optionItem {
  color: rgb(172, 172, 172);
}
.selected{
  color: black;
  font-weight: bold;
}
.sel-container  {
  position: relative;
}
.sel-container > span {
  position: absolute;
  bottom: 1px;
  right: 10px;
}
</style>
