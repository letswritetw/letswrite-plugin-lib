<template>
  <!-- App.vue -->
  <v-app>

    <!-- aside -->
    <v-navigation-drawer app v-model="drawer">

      <!-- 標題 -->
      <v-list-item to="/">
        <v-list-item-avatar>
          <v-img src="https://fakeimg.pl/180x180/?text=Logo"></v-img>
        </v-list-item-avatar>
        <v-list-item-content>
          <v-list-item-title class="title">
            套件集合站
          </v-list-item-title>
          <v-list-item-subtitle>
            Let's Write - Augustus
          </v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>

      <v-divider></v-divider>

      <!-- 選單 -->
      <v-list dense>
        <v-list-item
          v-for="(n, v) in asideNav"
          :key="v"
          :to="'/plugin-' + v"
        >
          <v-list-item-icon>
            <v-icon>mdi-{{ n.vicon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ n.name }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>

      <v-divider></v-divider>

      <!-- fb like 記得改掉 -->
      <v-list dense>
        <v-list-item>
          <div class="fb-like" data-href="https://plugins.letswrite.tw/" data-width="" data-layout="button_count" data-action="like" data-size="small" data-show-faces="true" data-share="true"></div>
        </v-list-item>
      </v-list>

    </v-navigation-drawer>

    <v-app-bar app color="blue" dark collapse>
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
      <v-btn icon target="_blank" href="https://letswrite.tw/">
        <v-icon>mdi-github-circle</v-icon>
      </v-btn>
    </v-app-bar>



    <!-- Sizes your content based upon application components -->
    <v-content>

      <!-- Provides the application the proper gutter -->
      <v-container fluid>

        <!-- If using vue-router -->
        <router-view></router-view>
      </v-container>
    </v-content>



    <v-footer app class="justify-center">
      <h6>&copy; {{ new Date().getFullYear() }} by Let's Write</h6>
    </v-footer>


  </v-app>
</template>

<script>
  export default {
    data() {
      return {
        drawer: true,
        asideNav: []
      }
    },
    created() {
      // yourFirebaseProject 要替換成你的 firebase project 名稱
      fetch('https://yourFirebaseProject.firebaseio.com/nav.json').then(res => res.json())
        .then(res => this.asideNav = res);
    }
  }
</script>