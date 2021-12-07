<template>
  <button :id="audioName" class="drum-pad" @click="playSound">
    {{ title }}
    <audio :id="title" class="clip" :src="audioTrack"></audio>
  </button>
</template>

<script>
export default {
  emits: ["setDisplayValue"],
  props: ["title", "audioTrack", "id", "audioName"],
  methods: {
    playSound() {
      let audio = document.getElementById(this.title);
      audio.play();
      this.$emit("setDisplayValue", this.audioTrackName);
    },
  },
  data() {
    return {
      audioTrackName: this.audioName,
    };
  },
};
</script>

<style>
.drum-pad {
  background-color: #3c354a;
  border: none;
  text-decoration: none;
  color: #fff;
  border: 1px solid rgba(255, 255, 255, 0.5);
  border-radius: 5px;
  height: 70px;
  width: 70px;
}

.drum-pad:active {
  transform: scale(0.96);
}
</style>