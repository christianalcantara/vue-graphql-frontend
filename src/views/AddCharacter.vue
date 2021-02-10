<template>

  <v-form v-on:submit.prevent="formValid"
          ref="form"
          v-model="valid"
          lazy-validation
          style="width: 50%"
  >
    <v-text-field
        v-model="name"
        :counter="40"
        :rules="nameRules"
        label="Name"
        required
        outlined
    ></v-text-field>

    <v-textarea
        v-model="description"
        label="Description"
        required
        outlined
    ></v-textarea>
    <v-file-input
        v-model="thumbnail"
        :rules="thumbnailRules"
        label="Thumbnail"
        counter
        show-size
        truncate-length="21"
        required
        outlined
    ></v-file-input>
    <v-alert
        v-model="erro"
        dense
        type="error"
    >
      {{ errMsg }}
    </v-alert>

    <v-btn
        class="mt-3 ma-2"
        :disabled="!valid || loading"
        :loading="loading"
        color="success"
        @click="submit"
    >
      Submit
      <v-icon class="ml-2">mdi-send</v-icon>
    </v-btn>
  </v-form>

</template>

<script>
import CreateCharacter from '../graphql/CreateCharacter.gql'
import UploadFile from '../graphql/UploadFile.gql'

export default {
  name: "AddCharacter",
  data: () => ({
    loading: false,
    valid: false,
    erro: false,
    errMsg: '',
    name: '',
    nameRules: [
      v => !!v || 'Name is required',
      v => (v && v.length <= 40) || 'Name must be less than 40 characters',
    ],
    description: '',
    thumbnail: '',
    thumbnailRules: [
      v => !!v || 'Image is required',
    ],
  }),
  computed: {
    formValid() {
      return this.valid
    },
  },
  methods: {
    validate() {
      this.$refs.form.validate()
    },
    reset() {
      this.$refs.form.reset()
    },
    resetValidation() {
      this.$refs.form.resetValidation()
    },
    async submit() {
      this.validate()
      if ((!this.name) || (!this.thumbnail)) {
        console.log('>>')
      } else {
        const {name, description, thumbnail} = this.$data
        this.loading = true
        console.log(name, description)
        console.log(thumbnail)
        await this.$apollo.mutate({
          mutation: CreateCharacter,
          variables: {
            name,
            description
          }
        })
            .then((data) => {
              this.erro = false
              this.errMsg = ''
              const pk = data.data.createCharacter.character.id
              this.$apollo.mutate({
                mutation: UploadFile,
                variables: {
                  pk,
                  file: thumbnail
                }
              })
                  // eslint-disable-next-line no-unused-vars
                  .then((data) => {
                    this.erro = false
                    this.errMsg = ''
                    this.$router.push('/');
                  })
                  .catch((err) => {
                    this.erro = true
                    this.errMsg = err
                  })
            })
            .catch((err) => {
              this.erro = true
              this.errMsg = err
            })
        this.loading = false
      }

    }
  },
}
</script>

<style scoped>

</style>