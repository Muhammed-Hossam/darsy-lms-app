<template>
  <v-app-bar class="py-3 px-3 position-fixed" flat :class="appBarShadow">
    <v-app-bar-nav-icon
      class="d-md-none"
      @click="toggleDrawer"
    ></v-app-bar-nav-icon>
    <v-app-bar-title class="d-none d-md-block">
      <router-link to="/" class="logo">
        <img
          src="../../assets/logo.png"
          width="70"
          height="70"
          class="mt-2"
          alt="app-logo"
        />
      </router-link>
    </v-app-bar-title>
    <v-list nav role="navigation" class="d-none d-md-flex flex-row ga-3">
      <v-list-item to="/" variant="text" color="green-lighten-1" class="text-h6"
        >الصفحة الرئيسية</v-list-item
      >
      <v-list-item
        to="/explore"
        variant="text"
        color="green-lighten-1"
        class="text-h6"
        >تصفََح</v-list-item
      >
    </v-list>
    <v-spacer></v-spacer>
    <v-spacer></v-spacer>
    <v-text-field
      prepend-inner-icon="mdi-magnify"
      variant="solo-filled"
      density="compact"
      bg-color="grey-lighten-3"
      placeholder="ابحث"
      role="search"
      type="text"
      name="search"
      :model-value="searchValue"
      rounded
      flat
      hide-details
      :center-affix="true"
      @update:focused="isSearchFocused = !isSearchFocused"
      :direction="isSearchFocused ? 'horizontal' : 'vertical'"
    >
    </v-text-field>
    <v-spacer></v-spacer>
    <v-spacer></v-spacer>
    <v-list class="d-none d-md-block">
      <v-btn
        to="/register"
        variant="flat"
        rounded="xl"
        color="green-lighten-1"
        class="ml-3"
        >سجل مجاناً</v-btn
      >
      <v-btn
        to="login"
        variant="flat"
        rounded="xl"
        color="green-lighten-1"
        class="ml-3"
        >دخول</v-btn
      >
    </v-list>
    <v-btn :icon="themeIcon" @click="toggleTheme"></v-btn>
  </v-app-bar>

  <v-navigation-drawer v-model="drawer" location="right" class="d-md-none">
    <router-link to="/" class="logo">
      <v-app-bar-title class="mt-5 text-center border-b">
        <img
          src="../../assets/logo.png"
          width="70"
          height="70"
          class="mt-2"
          alt="app-logo"
        />
      </v-app-bar-title>
    </router-link>
    <v-list nav class="mt-5">
      <v-list-item
        to="/"
        prepend-icon="mdi-home"
        variant="text"
        color="green-lighten-1"
        class="text-h6"
        >الصفحة الرئيسية</v-list-item
      >
      <v-list-item
        to="/explore"
        prepend-icon="mdi-compass"
        variant="text"
        color="green-lighten-1"
        class="text-h6"
        >تصفح</v-list-item
      >
      <v-list-item
        to="/register"
        prepend-icon="mdi-account-plus"
        variant="text"
        color="green-lighten-1"
        class="text-h6"
        >سجل مجاناً</v-list-item
      >
      <v-list-item
        to="/login"
        prepend-icon="mdi-login"
        variant="text"
        color="green-lighten-1"
        class="text-h6"
        >دخول</v-list-item
      >
    </v-list>
  </v-navigation-drawer>
</template>

<script setup>
import { ref, watch, computed } from "vue";
import { useTheme } from "vuetify";

const searchValue = ref("");
const isSearchFocused = ref(false);

/** Start AppBar shadow effect when scrolling **/
const appBarShadow = ref("");
const scrollYValue = ref(window.scrollY);

// update the reactive reference of "scrollYValue" when window is scrolled
window.addEventListener("scroll", () => {
  scrollYValue.value = window.scrollY;
});

watch(scrollYValue, (newScrollValue) => {
  if (newScrollValue > 0) {
    appBarShadow.value = "shadow-lg";
  } else {
    appBarShadow.value = "";
  }
});
/** End AppBar shadow effect when scrolling **/

/** Start Navigation Drawer **/
const drawer = ref(false);
const toggleDrawer = () => (drawer.value = !drawer.value);
/** End Navigation Drawer **/

/** start Toggle Theme **/
const theme = useTheme();

function toggleTheme() {
  theme.global.name.value = theme.global.current.value.dark ? "light" : "dark";
}
const themeIcon = computed(() =>
  theme.global.current.value.dark
    ? "mdi-white-balance-sunny"
    : "mdi-weather-night"
);
/** End Toggle Theme **/
</script>

<style lang="scss" scoped>
$primary-color: #7ed957;

// .elevation-3.v-theme--light {
//   box-shadow: 0 10px 30px rgba(0, 0, 0, 0.11) !important;
// }

.v-toolbar {
  &.v-theme--light {
    background-color: #fff !important;
  }
}
</style>
