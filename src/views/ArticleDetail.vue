<template>
  <v-card flat v-if="article && article.image">
    <v-img height="400" :src="article.image.url"></v-img>

    <v-card-title>{{ article.title }}</v-card-title>

    <v-card-text>
      <div v-html="sanitizedBody"></div>
    </v-card-text>
  </v-card>
</template>


<script>
import axios from "axios";
import sanitizeHtml from "sanitize-html";

export default {
  name: "ArticleDetail",

  data: () => ({
    article: {}
  }),

  computed: {
    sanitizedBody() {
      // imgタグのみ使えるようにする
      return sanitizeHtml(this.article.body, {
        allowedTags: sanitizeHtml.defaults.allowedTags.concat(["img"])
      });
    }
  },

  async mounted() {
    //記事の取得
    await axios.get('https://nepnep.microcms.io/api/v1/articles', {
      headers: { 'X-API-KEY': process.env.VUE_APP_X_API_KEY}
    })
    .then((response) => {
      // APIから取得した記事の配列から最初の記事を取得
      const firstArticle = response.data.contents[0];
      // this.articleにセット
      this.article = firstArticle;
    });
  }

};
</script>