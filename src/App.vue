<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
          transition="scale-transition"
          width="40"
        />

       <h2>雑誌</h2>
      </div>

      <v-spacer></v-spacer>
      <v-btn text to="/" tag="router-link">商品一覧</v-btn>
      <v-btn text to="/history" tag="router-link">購入履歴</v-btn>
    </v-app-bar>

    <v-main>
      <router-view/>
    </v-main>
  </v-app>
</template>

<script>