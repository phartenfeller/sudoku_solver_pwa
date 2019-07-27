<template>
  <div id="app">
    <meta name="theme-color" content="#f6ad55" />
    <link
      href="https://fonts.googleapis.com/css?family=Poppins:300,400,600&display=swap"
      rel="stylesheet"
    />
    <Navbar />
    <HelloWorld msg="Welcome to Your Vue.js App" class="flex-1" />
    <Footer />
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import Navbar from "./components/Navbar.vue";
import Footer from "./components/Footer.vue";
import "./assets/css/tailwind.css";

export default {
  name: "app",
  components: {
    Navbar,
    HelloWorld,
    Footer
  }
};
</script>

<style>
body {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  @apply font-sans bg-orange-100;
}

body,
html,
#app {
  @apply flex h-full flex-col;
}
</style>
