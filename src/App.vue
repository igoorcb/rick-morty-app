<template>
  <div class="app">
    <CharacterList @viewDetails="viewDetails" />
  </div>
</template>

<script>
import CharacterList from './components/CharacterList.vue';
export default {
  components: { CharacterList },
  setup() {
    const viewDetails = character => {
      alert(`Name: ${character.name}\nStatus: ${character.status}\nEpisodes: ${character.episode.length}`);
    };
    return { viewDetails };
  },
};
</script>

<style>
body {
  background: #111;
  color: white;
  margin: 0;
  font-family: Arial, sans-serif;
}

.app {
  text-align: center;
  padding: 20px;
}
</style>