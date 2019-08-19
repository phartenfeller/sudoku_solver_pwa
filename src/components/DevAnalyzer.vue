<template>
  <div>
    <h1>DevAnalyzer</h1>
    <div>Filename: {{fileObject.name}}</div>
    <img ref="imageDisplay" :src="imageSrc" class="hidden" />
    <div>width: {{width}} height: {{height}}</div>
    <canvas ref="imageCanvas" class="max-h-screen max-w-full" />
    <h2>Fields</h2>
    <div class="w-full">
      <div v-for="i in 9" :key="i" class="block">
        <canvas
          class="inline-block w-1/12 border border-pink-300 hover:border-pink-600"
          v-for="j in 9"
          :ref="`tile_canvas_r${i}`"
          :key="j"
        />
      </div>
    </div>
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

      const fieldW = parseInt(w / 9);
      const fieldH = parseInt(h / 9);
      const borderW = parseInt(fieldW / 5);
      const borderH = parseInt(fieldH / 5);

      const windowWidth = window.innerWidth;
      const dpw = parseInt(windowWidth / 9) - 1;

      console.log(`${fieldW} x ${fieldH}`);

      let currentCanvas;
      let ref;

      for (let i = 1; i <= 9; i++) {
        for (let j = 0; j < 9; j++) {
          ref = `tile_canvas_r${i}`;
          console.log("ref =>", ref);
          currentCanvas = this.$refs[ref][j];

          if (currentCanvas) {
            currentCanvas.width = fieldW;
            currentCanvas.height = fieldW;

            currentCanvas
              .getContext("2d")
              .drawImage(
                imageCanvas,
                fieldW * j + borderW,
                fieldH * (i - 1) + borderH,
                fieldW - borderW,
                fieldH - borderH,
                0,
                0,
                fieldW,
                fieldW
              );
          } else {
            console.log("not found");
          }
        }
      }
    }
  }
};
</script>