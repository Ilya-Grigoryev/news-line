<template>
  <v-app>
    <v-navigation-drawer
      style="position:fixed; top:0; left:0; overflow-y:scroll;"
      v-model="drawer"
      
      app
    >
      <v-list nav dense>

        <v-list-item-group
          v-model="group"
          active-class="deep-purple--text text--accent-4"
        >

        <v-list-item link @click="newLang('us')">
          <v-list-item-content>
            <v-list-item-title>• Ameriсan</v-list-item-title>
          </v-list-item-content>
        </v-list-item>

        <v-list-item link @click="newLang('ru')">
          <v-list-item-content>
            <v-list-item-title>• Russian</v-list-item-title>
          </v-list-item-content>
        </v-list-item>

        <v-list-item link @click="newLang('ua')">
          <v-list-item-content>
            <v-list-item-title>• Ukrainian</v-list-item-title>
          </v-list-item-content>
        </v-list-item>

        <v-list-item link @click="newLang('de')">
          <v-list-item-content>
            <v-list-item-title>• German</v-list-item-title>
          </v-list-item-content>
        </v-list-item>

        <v-list-item link @click="newLang('bg')">
          <v-list-item-content>
            <v-list-item-title>• Bulgarian</v-list-item-title>
          </v-list-item-content>
        </v-list-item>

        <v-list-item link @click="newLang('gb')">
          <v-list-item-content>
            <v-list-item-title>• Great British</v-list-item-title>
          </v-list-item-content>
        </v-list-item>

        <v-list-item link @click="newLang('tr')">
          <v-list-item-content>
            <v-list-item-title>• Turkish</v-list-item-title>
          </v-list-item-content>
        </v-list-item>

        </v-list-item-group>
      </v-list>
    </v-navigation-drawer>

    <v-system-bar color="deep-purple darken-3"></v-system-bar>

    <v-app-bar app color="indigo" dark>

      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />

      <v-toolbar-title>News</v-toolbar-title>


        <v-col   md="5" @keyup.enter="Search()">
          <v-text-field
            v-model="inquiry"
            label="Enter keyword and press 'Enter'"
            lined
          ></v-text-field>
        </v-col>


    </v-app-bar>
    <v-content>
    
      <NewsLine v-for="post in news" 
        :key="post.title" 
        :title="post.title" 
        :description="post.description" 
        :urlToImage="post.urlToImage" 
        :url="post.url"
        :publishedAt="post.publishedAt">
      {{post.author}}</NewsLine>

    </v-content>
    <v-footer color="indigo" app>
      <span class="white--text">&copy; 2019</span>
    </v-footer>
  </v-app>
</template>

<script>
import NewsLine from './components/NewsLine';

export default {
  name: 'App',

  components: {
    NewsLine,
  },

  data: () => ({
    news: [],
    source: '',
    lang_href: '',
    inquiry: '',
    lang: 'us',
    drawer: null,
    group: 0,
  }),

  watch: {
      group () {
        this.drawer = null
      },
    },

  methods:{
    newLang(lang){
      this.lang = lang
      this.getNewHref()
    },
    getNews(){
      this.axios.get(this.lang_href)
      .then((response) => {
        this.news = response.data.articles
        console.log(response)
      })
    },
    Search(){
      this.getNewHref()
    },
    getNewHref(){
      this.lang_href = 'https://newsapi.org/v2/top-headlines?country='+this.lang+
              '&apiKey=d7f41a32c26b4bbfb596d58b1a54c766'+'&q='+this.inquiry;

      this.getNews()
    }
  },
  mounted() {
    this.getNewHref()
  },
};
</script>
