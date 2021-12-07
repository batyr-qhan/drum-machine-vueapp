<template>
  <div id="drum-machine">
    <ul class="drum-list">
      <drum-button
        v-for="drum in drums"
        :key="drum.id"
        :title="drum.name"
        :audioTrack="drum.audio"
        :id="drum.id"
        :audioName="drum.audioName"
        @setDisplayValue="setDisplayValue"
      ></drum-button>
    </ul>
    <div id="display">{{ displayValue }}</div>
  </div>
</template>

<script>
import drums from "./assets/drums";
import DrumButton from "./components/DrumButton.vue";

export default {
  name: "App",
  components: {
    DrumButton,
  },
  data() {
    return {
      drums: drums,
      displayValue: "",
    };
  },
  methods: {
    setDisplayValue(val) {
      console.log(val);
      this.displayValue = val;
    },
    handleKeyDown(e) {
      let key = e.key.toUpperCase();
      let audio = document.getElementById(key);
      audio.play();
      this.setDisplayValue(audio.parentNode.id);
    },
  },
  created() {
    window.addEventListener("keydown", this.handleKeyDown);
  },
  unmounted() {
    window.removeEventListener("keydown", this.handleKeyDown);
  },
};
</script>

<style>
*,
*::before,
*::after {
  box-sizing: border-box;
}

* {
  margin: 0;
  padding: 0;
}

html,
body {
  height: 100%;
}

body {
  line-height: 1.5;
  -webkit-font-smoothing: antialiased;
  font-family: "Russo One", sans-serif;
}

img,
picture,
video,
canvas,
svg {
  display: block;
  max-width: 100%;
}

input,
button,
textarea,
select {
  font: inherit;
}

p,
h1,
h2,
h3,
h4,
h5,
h6 {
  overflow-wrap: break-word;
}

ul li {
  list-style: none;
}

#app {
  height: 100%;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #261e35;
}

#drum-machine {
  padding: 20px;
  display: flex;
  background: linear-gradient(to top right, #ff7a7a, #2a0fd3);
  border: 1px solid rgba(255, 255, 255, 0.5);
  border-radius: 20px;
}

.drum-list {
  padding: 20px;
  display: grid;
  grid-template-columns: repeat(3, 70px);
  gap: 1px;
}

#display {
  margin: 20px;
  padding: 5px;
  min-width: 100px;
  width: 150px;
  background-color: #3c354a;
  color: #fff;
  display: flex;
  justify-content: center;
  align-items: center;
  border: 1px solid rgba(255, 255, 255, 0.5);
  border-radius: 20px;
  height: 70px;
}
</style>
