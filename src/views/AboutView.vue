<template>
  <v-container>
      <v-row class="text-center">
      <v-col class="mb-4">
        <h1 class="display font-weight-bold">
          商品詳細
        </h1>
      </v-col>
    </v-row>

    <v-row justify="center">
        <v-card v-if="product" class="pa-6" elevation="6">
          <v-img src="https://via.placeholder.com/300x200" height="10px"></v-img>
          <v-card-title><strong>●出版社：</strong>{{ product.Publisher }}</v-card-title>
          <v-card-title><strong>●発売日：</strong>{{ product.Date }}</v-card-title>
          <v-card-title><strong>●言語：</strong>{{ product.Language }}</v-card-title>
          <v-card-title><strong>●おすすめ度：</strong>{{ product.Recommendation_score }}</v-card-title>
            <v-col cols="12">
              <div class="d-flex justify-center">
                <v-btn color="primary" class="mx-auto my-5" max-width="600" to="/" tag="router-link">商品一覧に戻る</v-btn>
              </div>
            </v-col>
        </v-card>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      product: null
    };
  },
  async mounted() {
    const id = this.$route.query.id;
    console.log('受け取ったID:', id);

    try {
      const response = await fetch(`https://m3h-koinuma-0606.azurewebsites.net/api/SELECT?id=${encodeURIComponent(id)}`);
      const text = await response.text();
      const json = JSON.parse(text);
      this.product = json.List.find(item => item.ID === id); // ← IDで1件だけ抽出


      console.log('取得した商品詳細:', this.product);
    } catch (error) {
      console.error('商品詳細の取得に失敗しました:', error);
    }
  }
}
</script>