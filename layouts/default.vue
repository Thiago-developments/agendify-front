<template>
  <v-app dark>
    <v-app-bar :clipped-left="clipped" fixed app>
      <img src="@/assets/icones/Logo.svg" alt="Logo" class="logo" />
      <v-spacer />
    </v-app-bar>
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: "DefaultLayout",
  data() {
    return {
      clipped: false,
      fixed: false,
    };
  },
};
</script>

<style>
.logo {
  height: 100%;
  width: auto;
  max-height: inherit;
  display: block;
  margin: auto;
}
</style>
