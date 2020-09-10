# Custom components

Test custom components using CSS

``` bash
# Table/Row
    <TableContainer>
        //elements
    </TableContainer>
```

``` bash
# Column
      <TableColumn>
        //elements
      </TableColumn>
```

``` bash
# Input text
        <InputText
          inputType='text|number|date|email'
          label='Label Example'
          :leftIcon="require('@/assets/icon.svg')"
          @left-icon-click="functionToCall"
          required
          :step='0.1'
          name='nameExample'
          :rightIcon="require('@/assets/icon.svg')"
          @right-icon-click="functionToCall"
          v-model="modelExample"
        />
```

``` bash
# File input
        <FileInput
          label='Label Example'
          name='nameExample'
          v-model="modelExample"
        />
```

``` bash
# Select input
        <Select
          label="Label Example"
          name="nameExample"
          :items="itemsArray"
          v-model="modelExample"
        />
```
``` bash
# button
        <Button @clickAction="functionToCall">
          Button Text
        </Button>
```

``` bash
# Textarea
        <TextArea
          v-model="modelExample"
          label="Label Example"
          name="nameExample"
          required
         />
```
