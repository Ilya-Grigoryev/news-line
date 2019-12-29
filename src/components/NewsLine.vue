<template>
<v-app>
  <v-content>
  <v-card
    max-width="344"
    class="mx-auto">
    <v-list-item>
      <!-- <v-list-item-avatar src='src/assets/def-avatar.png'></v-list-item-avatar> -->
      <v-list-item-content>
        <v-list-item-title class="headline">{{title}}</v-list-item-title>
        <v-list-item-subtitle><slot>Anonim</slot></v-list-item-subtitle>
      </v-list-item-content>
    </v-list-item>

    <v-img
      :src='urlToImage'
      height="194"
    ></v-img>

    <v-card-text>
      {{description}}
    </v-card-text>

    <v-card-actions>
      <v-btn outlined color="deep-purple accent-4" :href="url">read more about it</v-btn>

      <!-- <v-btn text color="deep-purple accent-4">Bookmark</v-btn> -->

      <v-spacer></v-spacer>
      <v-btn icon @click="like_counter++" v-bind:color="like_counter % 2 == 0 ? 'error' : 'grey'">
        <v-icon>mdi-heart</v-icon>
      </v-btn>
      <v-btn icon>
        <v-icon>mdi-share-variant</v-icon>
      </v-btn>
    </v-card-actions>
  </v-card>
  </v-content>
</v-app>
</template>

<script>
export default {
  props: ['title', 'description', 'urlToImage', 'url'],
  data: () => ({
    like_counter: 1
  }),
}
</script>