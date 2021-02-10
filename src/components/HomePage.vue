<template>

  <ApolloQuery
      :query="require('../graphql/Character.gql')"
  >
    <v-row slot-scope="{ result: { data } }"
           class="mb-3"
           no-gutters>
      <template v-if="data">
        <v-flex v-for="node of data.characters.edges"
                :key="node.node.id"
                class="xs12 sm4 md3" d-flex>
          <v-card class="mb-6">
            <v-avatar
                class="profile"
                color="grey"
                size="300"
                tile
            >
              <v-img
                  :src="node.node.thumbUrl"
                  class="white--text align-end"
              >
                <v-card-title>{{ node.node.name }}</v-card-title>
              </v-img>
            </v-avatar>
            <v-card-subtitle class="pb-0">

            </v-card-subtitle>

            <v-card-text class="text--primary" style="max-height: 150px; height: 150px">
              <div>{{ node.node.description || 'no description' }}</div>
            </v-card-text>

            <v-fab-transition>
              <v-btn
                  absolute
                  bottom
                  color="primary"
                  dark
                  fab
                  right
                  small
              >
                <v-icon>mdi-heart</v-icon>
              </v-btn>
            </v-fab-transition>
          </v-card>

        </v-flex>
      </template>
    </v-row>
  </ApolloQuery>

</template>

<script>
export default {
  name: 'HomePage',
  apollo: {},
  data: () => ({
    dialog: false
  }),
}
</script>
