<template>
  <div id="app">
    <img class="logo" src="@/assets/logo.png" alt="Logo" />
    <div class="container">
      <div v-if="music" class="grid">
        <SingleCard
          v-for="(music, index) in music"
          :musicData="music"
          :key="index"
        />
      </div>
      <div v-else>
        <h1>No</h1>
      </div>
    </div>
  </div>
</template>

<script>
import SingleCard from "./components/Card.vue";
import axios from "axios";

export default {
  name: "App",
  data() {
    return {
      music: null,
    };
  },
  components: {
    SingleCard,
  },
  mounted() {
    axios
      .get("https://flynn.boolean.careers/exercises/api/array/music")
      .then((response) => {
        this.music = response.data.response;
      });
  },
};
</script>

<style lang="scss">
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

html {
  background-color: #262626;
}

#app {
  font-family: sans-serif;
  color: black;

  .logo {
    position: fixed;
    top: 1rem;
    left: 1rem;
    width: 50px;
  }

  .container {
    max-width: 1100px;
    margin: 4rem auto;

    .grid {
      display: grid;
      grid-template-columns: repeat(5, minmax(0, 1fr));
      gap: 1rem;
    }
  }
}
</style>
