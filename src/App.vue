<template>
  <div id='app'>
    <TableContainer>
      <TableColumn>
        <InputText
          inputType='email'
          label='Example 1'
          :leftIcon="require('@/assets/test-icon.svg')"
          @left-icon-click="clickLeftIcon"
          required
          name='input1'
          v-model="results.inputWithText"
        />
      </TableColumn>
      <TableColumn>
        <InputText
          inputType='date'
          label='Example 2'
          name='input2'
          v-model="results.inputWithDate"
        />
      </TableColumn>
      <TableColumn>
        <InputText
          inputType='number'
          :step='0.1'
          label='Example 3'
          :rightIcon="require('@/assets/test-icon.svg')"
          @right-icon-click="clickRightIcon"
          name='input3'
          v-model="results.inputWithNumber"
        />
      </TableColumn>
      </TableContainer>
      <TableContainer>
      <TableColumn>
        <FileInput
          label='File Input'
          name='inputFile'
          v-model="results.inputFile"
        />
      </TableColumn>
      <TableColumn>
        <Select
          label="Combobox"
          name="Combobox"
          :items="comboboxArray"
          v-model="results.selectText"
        />
      </TableColumn>
      <TableColumn>
        <Button @clickAction="clickButton">
          Send
        </Button>
      </TableColumn>
      <TableColumn>
        <TextArea
          v-model="results.textAreaAux1"
          label="Example text area 1"
          name="TextArea 1"
          required
         />
      </TableColumn>
      <TableColumn>
        <TextArea
          v-model="results.textAreaAux2"
          label="Example text area 2"
          name="TextArea 2"
         />
      </TableColumn>
    </TableContainer>

    <p style="text-align:justify">
      <pre>{{ results }}</pre>
    </p>
  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      results: {
        inputWithText: 'a2@a.com',
        inputWithDate: '',
        inputWithNumber: '222',
        inputFile: null,
        textAreaAux1: '',
        textAreaAux2: '',
        selectText: '2'
      },
      comboboxArray: [
        {
          id: '1',
          name: 'Option 1'
        },
        {
          id: '2',
          name: 'Option 2'
        },
        {
          id: '3',
          name: 'Option 3'
        },
        {
          id: '4',
          name: 'Option 4'
        }
      ]
    }
  },
  methods: {
    clickRightIcon () {
      alert('clickRightIcon')
    },
    clickLeftIcon () {
      alert('clickLeftIcon')
    },
    clickButton () {
      alert('Button Click')
    }
  }
}
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

<style scoped>
.result div{
  display: inline-block;
}
</style>
