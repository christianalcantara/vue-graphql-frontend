<template>

  <ApolloQuery
      :query="require('../graphql/Character.gql')"
  >
    <v-row slot-scope="{ result: { data } }"
           no-gutters
           class="mb-3">
      <template v-if="data">
        <v-flex v-for="node of data.characters.edges"
                :key="node.node.id"
                d-flex class="xs12 sm4 md3">
          <v-card class="mb-6">
            <v-avatar
                class="profile"
                color="grey"
                size="300"
                tile
            >
            <v-img
                class="white--text align-end"
                :src="node.node.thumbUrl"
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

                  color="primary"
                  fab
                  dark
                  small
                  absolute
                  bottom
                  right
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
