<template>
  <div>
    <h1>DevAnalyzer</h1>
    <div>Filename: {{fileObject.name}}</div>
    <img ref="imageDisplay" :src="imageSrc" class="hidden" />
    <div>width: {{width}} height: {{height}}</div>
    <canvas ref="imageCanvas" class="max-h-screen max-w-full" />
    <h2>Fields</h2>
    <canvas ref="canv_0_0" />
  </div>
</template>

<script>
export default {
  name: "DevAnalyzer",
  props: {
    fileObject: {
      type: File,
      required: true
    }
  },
  data() {
    return {
      imageSrc: "",
      width: "",
      height: ""
    };
  },
  mounted: function() {
    this.updateImageSrc();
  },
  methods: {
    updateImageSrc: function() {
      const vm = this;
      const imageDisplay = this.$refs.imageDisplay;
      const reader = new FileReader();

      imageDisplay.onload = function() {
        const w = this.width;
        const h = this.height;
        vm.width = w;
        vm.height = h;

        vm.updateCanvas(w, h);
      };

      reader.addEventListener(
        "load",
        function() {
          if (imageDisplay) {
            vm.imageSrc = reader.result;
          } else {
            console.warn("no ref");
          }
        },
        false
      );

      reader.readAsDataURL(this.fileObject);
    },
    updateCanvas: function(w, h) {
      const imageDisplay = this.$refs.imageDisplay;
      const imageCanvas = this.$refs.imageCanvas;
      const canv_0_0 = this.$refs.canv_0_0;

      imageCanvas.width = w;
      imageCanvas.height = h;

      imageCanvas.getContext("2d").drawImage(imageDisplay, 0, 0, w, h);

      const fieldW = (w / 9).toFixed(0);
      const fieldH = (h / 9).toFixed(0);
      const borderW = (fieldW / 5).toFixed(0);
      const borderH = (fieldH / 5).toFixed(0);

      console.log(`${fieldW} x ${fieldH}`);

      canv_0_0.width = fieldW;
      canv_0_0.height = fieldH;

      canv_0_0
        .getContext("2d")
        .drawImage(
          imageCanvas,
          borderW,
          borderH,
          fieldW - borderW,
          fieldH - borderH,
          0,
          0,
          fieldW - borderW,
          fieldH - borderH
        );
    }
  }
};
</script>