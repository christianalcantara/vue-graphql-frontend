<template>
  <v-app>

    <v-app-bar
        app
        color="primary"
        dark
    >
      <div class="d-flex align-center">
        <v-img
            :src="require('../src/assets/logo.svg')"
            alt="Vuetify Logo"
            class="shrink mr-2"
            contain
            transition="scale-transition"
            width="40"
        />

        <h2>Super Hero</h2>
      </div>


      <v-btn class="ml-4"
             text
             to="/"
      >
        <span class="mr-2">Home</span>
      </v-btn>
      <v-spacer></v-spacer>

      <v-btn
          text
          to="add_character"
      >
        <span class="mr-2">Add</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <v-container fluid grid-list-md>
        <v-col cols="12">
          <v-layout justify-center row wrap>
            <router-view/>
          </v-layout>
        </v-col>
      </v-container>
    </v-main>
  </v-app>
</template>


