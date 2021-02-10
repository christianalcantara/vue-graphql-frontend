<template>
  <v-container fluid>
      <ApolloQuery
          :query="require('../graphql/Character.gql')"
          poll-interval="1000"
      >

        <v-row slot-scope="{ result: { data } }"
               dense
        >
          <template v-if="data">
            <v-col
                v-for="node of data.characters.edges"
                :key="node.node.id"
                cols="3"
            >
              <v-card>
                <v-img
                    :src="node.node.thumbUrl"
                    class="white--text align-end"
                    gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
                    height="200px"
                >
                  <v-card-title v-text="node.node.name"></v-card-title>
                </v-img>
                <v-card-subtitle>
                    <small>{{ node.node.description || 'NO DESCRIPTION' }}</small><br>
                </v-card-subtitle>
                <v-card-actions>
                  <v-spacer></v-spacer>

                  <v-btn icon disabled="true">
                    <v-icon>mdi-heart</v-icon>
                  </v-btn>

                  <v-btn icon>
                    <v-icon color="red">mdi-delete</v-icon>
                  </v-btn>

                  <v-btn icon>
                    <v-icon color="info">mdi-pen</v-icon>
                  </v-btn>
                </v-card-actions>
              </v-card>
            </v-col>

          </template>
        </v-row>
      </ApolloQuery>
  </v-container>


</template>

<script>
export default {
  name: 'HomePage',
  apollo: {},
  data: () => ({
    dialog: false,
    cards: [
      { title: 'Pre-fab homes', src: 'https://cdn.vuetifyjs.com/images/cards/house.jpg', flex: 12 },
      { title: 'Favorite road trips', src: 'https://cdn.vuetifyjs.com/images/cards/road.jpg', flex: 6 },
      { title: 'Best airlines', src: 'https://cdn.vuetifyjs.com/images/cards/plane.jpg', flex: 6 },
    ],
  }),
}
</script>
