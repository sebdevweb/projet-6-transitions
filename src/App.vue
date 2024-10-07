<script setup>
  import { ref } from 'vue'
  import FadeSlideTransition from './components/FadeSlideTransition.vue';
  import { shuffleArray } from '@/composable/shuffleArray';

  const showSpoiler = ref(false)
  const toggleSpoiler = () => showSpoiler.value = !showSpoiler.value

  const movies = ref([
    "Les évadés",
    "Le parrain",
    "Batman",
    "Pulp Fiction",
    "Forrest Gump",
    "Inception"
  ])

  const movie = ref('')
  const addMovie = () => {
    movies.value = [movie.value, ...movies.value]
    movie.value = ''
  }
  const removeMovie = (movie) => {
    movies.value = movies.value.filter(m => m !== movie)
  }
  const randomize = () => {
    movies.value = shuffleArray(movies.value)
  }

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
    <input type="text" v-model="movie" placeholder="Ajouter un film">
    <button :disabled="movie.length === 0" @click="addMovie">Ajouter</button>
    <ul>
      <TransitionGroup name="list">
        <li v-for="movie in movies" :key="movie">
          {{ movie }}
          <button class="secondary" @click="removeMovie(movie)">X</button>
        </li>
      </TransitionGroup>
    </ul>
    <button @click="randomize">Réorganiser</button>
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
        background-color: darkred;
        padding: 2rem;
        max-width: 600px;
        border-radius: 20px;
        transition: .5s;
        margin-bottom: 2rem;
        p {
          color: white;
          font-size: 20px;
        }
      }
      .list-enter-active,
      .list-leave-active,
      .list-move {
        transition: .5s ease;
      }
      .list-leave-active{
        position: absolute;
      }
      .list-enter-from,
      .list-leave-to {
        opacity: 0;
        transform: translateX(30px);
      }
    }
  }
</style>
