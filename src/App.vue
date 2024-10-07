<script setup>
  import { ref } from 'vue'
  import FadeSlideTransition from './components/FadeSlideTransition.vue';

  const showSpoiler = ref(false)
  const toggleSpoiler = () => showSpoiler.value = !showSpoiler.value

</script>

<template>
  <div class="container">
    <button @click="toggleSpoiler">Afficher / Masquer le spoiler</button>
    <FadeSlideTransition>
      <div v-if="showSpoiler" class="spoiler">
        <p>A la fin tout le monde meurt !</p>
      </div>
      <div v-else>
        <p>Voir une information qui gâche tout.</p>
      </div>
    </FadeSlideTransition>
  </div>
</template>

<style lang="scss">
  body {
    margin: 0;
    padding: 0;
    font-family: sans-serif;
    .container {
      height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;

      button {
        padding: 1rem;
        font-size: 16px;
        border: none;
        border-radius: 10px;
        background-color: crimson;
        color: white;
        font-weight: 700;
        letter-spacing: 1px;
        max-width: 300px;
        cursor: pointer;
        transition: .2s;
        &:hover {
          background-color: darkred;
          transition: .3s;
        }
      }
      .spoiler {
        margin-top: 2rem;
        background-color: lightcoral;
        padding: 2rem;
        max-width: 600px;
        border-radius: 20px;
        transition: .5s;
        p {
          color: white;
          font-size: 20px;
        }
      }
    }
  }
</style>
