<template>
  <div id="app">
    <meta name="theme-color" content="#f6ad55" />
    <link
      href="https://fonts.googleapis.com/css?family=Poppins:300,400,600&display=swap"
      rel="stylesheet"
    />
    <Navbar />
    <Uploader v-if="!imageLoaded" @uploadSuccess="imageUploaded" class="flex-1" />
    <div v-if="imageLoaded">
      <DevAnalyzer v-if="devMode" :fileObject="fileObject" class="flex-1" />
    </div>
    <Footer />
  </div>
</template>

<script>
import Uploader from "./components/Uploader.vue";
import Navbar from "./components/Navbar.vue";
import Footer from "./components/Footer.vue";
import DevAnalyzer from "./components/DevAnalyzer.vue";
import "./assets/css/tailwind.css";

export default {
  name: "app",
  components: {
    Navbar,
    Uploader,
    Footer,
    DevAnalyzer
  },
  data() {
    return {
      imageLoaded: false,
      fileObject: undefined
    };
  },
  methods: {
    imageUploaded: function(fileObject) {
      this.imageLoaded = true;
      this.fileObject = fileObject;
    }
  },
  computed: {
    devMode: function() {
      return process.env.NODE_ENV === "development";
    }
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
