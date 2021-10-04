<template>
  <!-- HOME STUFF -->
  <div v-if="!isPlaying" class="h-screen flex flex-col justify-center">
    <div>
      <h1 class="font-bold text-5xl mb-4">Reaction Test Timer</h1>
      <h2 class="font-medium text-3xl mb-8">
        How fast is YOUR reaction speed?
      </h2>
      <button
        class="
          px-32
          py-4
          font-bold
          text-4xl
          mb-8
          rounded-md
          bg-green-300
          text-white
        "
        @click="start"
      >
        PLAY
      </button>
      <!-- SCORE -->
      <div v-show="reactionTime">
        <h1 class="font-medium text-3xl mb-8">Time: {{ reactionTime }}</h1>
      </div>
    </div>
  </div>
  <!-- REACTION TEST -->
  <ReactionTest v-if="isPlaying" :delay="delay" @end="handleEnd"></ReactionTest>
</template>

<script>
import ReactionTest from "./components/ReactionTest.vue";
export default {
  name: "App",
  components: { ReactionTest },
  data() {
    return {
      isPlaying: false,
      delay: null,
      reactionTime: null,
    };
  },
  methods: {
    start() {
      this.delay = 2000 + Math.random() * 5000;
      this.isPlaying = true;
    },
    handleEnd(reactionTime) {
      this.isPlaying = false;

      if (reactionTime === null) {
        this.reactionTime = "Clicked Too Early";
        return;
      }
      console.log("TEDSFDASF");
      this.reactionTime = reactionTime.toString() + " ms";
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
