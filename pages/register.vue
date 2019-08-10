<template>
  <v-layout align-center justify-center mt-10>
    <v-flex class="text-center" lg7 md7 xs12 sm12>
      <h1>Cadastro</h1>
      <form>
      <v-text-field
        v-model="name"
        label="Name"
        required
      ></v-text-field>
      <v-text-field
        v-model="email"
        label="E-mail"
        required
      ></v-text-field>
      <v-select
        v-model="select"
        :items="items"
        label="Select"
        required
      ></v-select>
      <v-checkbox
        v-model="checkbox"
        value="1"
        label="Option"
        type="checkbox"
        required
      ></v-checkbox>
  
      <v-btn class="mr-4" @click="submit">submit</v-btn>
      <v-btn @click="clear">clear</v-btn>
    </form>
    </v-flex>
  </v-layout>
</template>


<script>

export default {
  data () {
    return {
      name: '',
      email: '',
      select: null,
      items: [
        'Item 1',
        'Item 2',
        'Item 3',
        'Item 4',
      ],
      checkbox: null,
      dictionary: {
        attributes: {
          email: 'E-mail Address',
          // custom attributes
        },
        custom: {
          name: {
            required: () => 'Name can not be empty',
            max: 'The name field may not be greater than 10 characters',
            // custom messages
          },
          select: {
            required: 'Select field is required',
          },
        },
      },
      }
  }
,

  methods: {
    clear () {
      this.name = ''
      this.email = ''
      this.select = null
      this.checkbox = null
      this.$validator.reset()
    },
  }
}
</script>