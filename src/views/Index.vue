<template>
  <v-container>
    <v-layout text-center wrap>

      <v-flex mb-5 xs12>
        <h1 class="display-2 font-weight-bold mb-5">
          套件集合站
        </h1>
        <p>Let's Write Augustus 整理的套件收集網站。</p>
        <p>點選左側項目可以顯示套件的引用路徑，以及使用方法。</p>
        <p>有時間會陸續更新本站，畢竟寫使用方式需要時間。</p>
      </v-flex>

      <v-flex mb-5 xs12>
        <h2 class="headline font-weight-bold mb-3">Let's Write</h2>
        <p>Augustus, 前端工程師的學習筆記</p>
        <v-btn color="blue" dark link large target="_blank" href="https://letswrite.tw/">造訪官網</v-btn>
      </v-flex>

    </v-layout>
  </v-container>
</template>

<script>
export default {
  created() {
    // ga id 記得替換
    gtag('config', 'UA-111103074-1', {
      'page_title': '套件集合站 - Let\'s Write',
      'page_location': location.origin,
      'page_path': '/'
    });
  }
}
</script>