<template>
  <div
    class="
      w-screen
      h-screen
      bg-red-500
      cursor-pointer
      content-center
      flex flex-col
      justify-center
    "
    :class="{ ready: ready }"
    @click="stopTimer"
  >
    <div class="text-white text-4xl font-bold font-mono">
      <h1 v-show="!ready">CLICK WHEN GREEN</h1>
      <h1 v-show="ready">GO</h1>
    </div>
  </div>
</template>

<script>
export default {
  props: ["delay"],
  data() {
    return {
      ready: false,
      reactionTime: 0,
    };
  },
  mounted() {
    console.log("BLOCK MOUNTED");
    setTimeout(() => this.startTimer(), this.delay);
  },
  emits: ["end"],
  methods: {
    startTimer() {
      this.ready = true;
      this.reactionTime = new Date();
    },
    stopTimer() {
      const currentTime = new Date(); // Done first for accuracy
      if (this.ready === false) {
        this.$emit("end", null);
        return;
      }
      this.reactionTime = currentTime - this.reactionTime;
      this.ready = false;
      console.log("Reaction time: ", this.reactionTime);
      this.$emit("end", this.reactionTime);
    },
  },
};
</script>

<style scoped>
.ready {
  @apply bg-green-500;
}
</style>
