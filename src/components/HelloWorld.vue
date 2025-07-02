<template>
  <v-container>
    <v-row class="text-center">
      <v-col class="mb-4">
        <h1 class="display font-weight-bold">
          商品一覧
        </h1>
      </v-col>
    </v-row>
   
<v-row>
 <v-col
 v-for="item in products"
 :key="item.id"
 cols="12"
 sm="6"
 md="4"
 >
 
   <v-card>
    <v-img src="https://via.placeholder.com/300x200" height="100px"></v-img>
    <v-card-title>{{ item.name }}</v-card-title>
    <v-card-subtitle>{{ item.price }}</v-card-subtitle>
    <v-card-actions>
      <v-btn color="primary" @click="showDetails(item.id)">商品詳細</v-btn>
      <v-btn color="primary" @click="purchase(item.id)">購入する</v-btn>
    </v-card-actions>
   </v-card>
 </v-col>
</v-row>
 
 </v-container>
</template>
 
<script>
export default {
  data() {
    return {
      products: [], // 表示用の配列
      showDialog: false,
      selectedProduct: null
    };
  },
  mounted() {
    this.fetchData();
  },
  methods: {
    async fetchData() {
      try {
        const response = await fetch('https://m3h-koinuma-0606.azurewebsites.net/api/SELECT?');
        const text = await response.text(); // Spring BootはStringを返しているのでまずはtextで受け取る
        const json = JSON.parse(text); // 文字列をJSONに変換
        this.products = json.List; // "List"キーの中身を取り出す
      } catch (error) {
        console.error('データ取得エラー:', error);
      }
    },
    showDetails(id) {
      this.selectedProduct = this.products.find(p => p.id === id);
      this.showDialog = true;
    },
    purchase(id) {
      alert(`商品ID ${id} を購入します`);
    }
  }
};
</script>