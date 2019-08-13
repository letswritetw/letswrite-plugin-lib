<template>
  <v-container>
    <v-layout wrap>
      <v-flex md2></v-flex>
      <v-flex mb-5 md8 xs12>
        <h1 class="display-2 font-weight-bold mb-5 text-center">
          {{ article.name }}
          <v-btn v-if="article.src" text icon color="blue" link target="_blank" :href="article.src">
            <v-icon>mdi-open-in-new</v-icon>
          </v-btn>
        </h1>

        <v-divider class="mb-5"></v-divider>

        <h2 class="headline font-weight-bold mb-3">引用檔案</h2>
         <v-list-item two-line v-for="(f, i) in article.files" :key="i">
          <v-list-item-content>
            <v-text-field :id="i" :label="i" :value="f"></v-text-field>
          </v-list-item-content>
          <v-list-item-action>
            <v-btn color="blue js-copy" dark :data-clipboard-target="'#' + i">
              copy
              <v-icon right>mdi-content-copy</v-icon>
            </v-btn>
          </v-list-item-action>
        </v-list-item>

        <h2 class="headline font-weight-bold mb-3">使用方式</h2>

        <!-- yourCodepenId 要替換成你的 codepen id -->
        <iframe height="500" scrolling="no" :title="article.how" :src="'//codepen.io/yourCodepenId/embed/' + article.how + '/?height=500&theme-id=14916&default-tab=html&embed-version=2'" frameborder="no" allowtransparency="true" allowfullscreen="true" style="width: 100%;">See the Pen <a :href="'https://codepen.io/yourCodepenId/pen/' + article.how + '/'">{{ article.how }}</a> by sean (<a href='https://codepen.io/yourCodepenId'>@sean-su</a>) on <a href='https://codepen.io'>CodePen</a>.</iframe>

      </v-flex>
      <v-flex md2></v-flex>

      <!-- snackbar -->
      <v-snackbar top :timeout="snackTimeout" v-model="snackbar">
        {{ snackbarText }}
        <v-btn
          text
          @click="snackbar = false"
        >
          關閉
        </v-btn>
      </v-snackbar>

    </v-layout>
  </v-container>
</template>

<script>
  export default {
    data() {
      return {
        id: null,
        article: {},
        snackTimeout: 3000,
        snackbarText: '',
        snackbar: false
      }
    },
    methods: {
      triggerRouter() {
        this.id = this.$route.params.pathMatch;

        // yourFirebaseProject 要替換成你的 firebase project 名稱
        fetch('https://yourFirebaseProject.firebaseio.com/article/' + this.id + '.json').then(res => res.json())
          .then(res => {
            this.article = res;
            // ga id 記得替換
            gtag('config', 'UA-111103074-1', {
              'page_title': this.article.name,
              'page_location': location.origin,
              'page_path': location.pathname
            });
          });
      }
    },
    created() {
      this.triggerRouter();

      // use ClipboardJS plugin https://clipboardjs.com/
      const clipboard = new ClipboardJS('.js-copy');
      clipboard.on('success', () => {
        this.snackbarText = '連結已複製進剪貼薄';
        this.snackbar = true;
      });
    },
    watch: {
      '$route': 'triggerRouter'
    }
  };
</script>
