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
 :key="item.ID"
 cols="12"
 sm="6"
 md="4"
 >
 
   <v-card>
    <v-img src="https://via.placeholder.com/300x200" height="100px"></v-img>
    <v-img :src="item.Url" height="400px"></v-img>
    <v-card-title>{{ item.Name }}</v-card-title>
    <v-card-subtitle>{{ item.Price }}</v-card-subtitle>
    <v-card-actions>
      <v-btn color="primary" @click="showDetails(item.ID)">商品詳細</v-btn>
      <v-btn color="primary" @click="purchaseProduct(item.Name)">購入する</v-btn>
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
      products: [],
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
        const text = await response.text();
        const json = JSON.parse(text);
        this.products = json.List;
        
        // ここで中身を確認
        console.log('取得した商品データ:', this.products);

      } catch (error) {
        console.error('データ取得エラー:', error);
      }
    },
    showDetails(id) {
      this.$router.push({ name: 'about', query: {id} });
    },
    purchaseProduct(Name) {
      alert(`${Name} を購入します`);
    }
  }
};
</script>