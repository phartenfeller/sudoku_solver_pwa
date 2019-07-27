<template>
  <div>
    <p
      class="text-3xl text-center px-16 text-gray-800 mt-24 leading-tight"
    >Solve your Sudokus by scanning them with this app.</p>
    <div class="mt-16">
      <div class="text-gray-700 text-lg w-7/12 mx-auto font-light">Try it out:</div>
      <button class="action-btn">Camera</button>
      <button v-on:click="triggerFileUpload" class="action-btn">Gallery</button>
      <input
        type="file"
        ref="fileInput"
        accept="image/*"
        v-on:change="fileChange($event.target.files)"
        class="hidden"
      />
    </div>
  </div>
</template>

<script>
const STATUS_NONE = 0,
  STATUS_UPLOADING = 1,
  STATUS_SUCCESS = 2,
  STATUS_ERROR = 3,
  STATUS_EMPTY_FILE = 4;

export default {
  name: "HelloWorld",
  data() {
    return {
      uploadPicture: undefined,
      uploadStatus: STATUS_NONE
    };
  },
  methods: {
    triggerFileUpload: function() {
      if (this.$refs.fileInput) {
        this.$refs.fileInput.click();
      } else {
        console.error("fileInput not available");
      }
    },
    fileChange: function(fileArray) {
      const file = fileArray[0];
      console.log("file =>", file);
      if (!file) {
        console.warn("Empty File");
        this.uploadStatus = STATUS_EMPTY_FILE;
        return;
      }
      this.fileUpload(file);
    },
    fileUpload: function(formData) {
      this.uploadStatus = STATUS_UPLOADING;
      try {
        this.uploadPicture = formData;
        this.uploadStatus = STATUS_SUCCESS;
      } catch (error) {
        console.error(error);
        this.uploadStatus = STATUS_ERROR;
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.action-btn {
  @apply bg-orange-400 border-orange-600 rounded py-2 px-2 text-black block mx-auto mb-6 mt-1 text-lg border-b-4  w-7/12 font-light;
}

.action-btn:hover {
  @apply bg-orange-500;
}

.action-btn:focus {
  @apply outline-none bg-orange-500;
}

.action-btn:active {
  @apply bg-orange-600 shadow-inner;
}
</style>
