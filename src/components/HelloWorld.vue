<template>
  <div>
    <p
      class="text-3xl text-center px-16 text-gray-800 mt-24 leading-tight"
    >Solve your Sudokus by scanning them with this app.</p>
    <div class="mt-16">
      <div class="text-gray-700 text-lg w-7/12 mx-auto font-light">Try it out:</div>
      <button class="action-btn">Camera</button>
      <button class="action-btn">Gallery</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String
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
