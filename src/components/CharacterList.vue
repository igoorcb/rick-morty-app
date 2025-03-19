<template>
  <div class="container">
    <h1>The Rick and Morty API</h1>
    <div class="search-bar">
      <SearchBar @search="updateSearch" />
      <select v-model="status">
        <option value="">Todas</option>
        <option value="Alive">Vivas</option>
        <option value="Dead">Mortas</option>
        <option value="unknown">Desconhecidas</option>
      </select>
    </div>
    <p>Total de Personagens: {{ total }}</p>
    <p>Total de Personagens Filtrados: {{ filteredCharacters.length }}</p>

    <div class="character-grid">
      <div v-for="(character, index) in filteredCharacters" :key="character.id" class="grid-item">
        <character-card :character="character" @viewDetails="$emit('viewDetails', character)" />
      </div>
    </div>
  </div>
</template>

<script>
import { ref, computed, onMounted } from 'vue';
import CharacterCard from './CharacterCard.vue';
import SearchBar from './SearchBar.vue';

export default {
  components: {
    CharacterCard,
    SearchBar
  },
  emits: ['viewDetails'],
  setup() {
    const characters = ref([]);
    const search = ref('');
    const status = ref('');
    const total = ref(0);

    const fetchCharacters = async () => {
      try {
        const res = await fetch('https://rickandmortyapi.com/api/character');
        const data = await res.json();
        characters.value = data.results;
        total.value = data.info.count; 
      } catch (error) {
        console.error('Erro ao buscar personagens:', error);
      }
    };

    onMounted(fetchCharacters);

    const filteredCharacters = computed(() => {
      return characters.value.filter(c =>
        c.name.toLowerCase().includes(search.value.toLowerCase()) &&
        (status.value ? c.status === status.value : true)
      );
    });

    const updateSearch = (query) => {
      search.value = query;
    };

    return {
      characters,
      search,
      status,
      total,
      filteredCharacters,
      updateSearch
    };
  },
};
</script>

<style scoped>
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}

h1 {
  text-align: center;
  color: white;
  margin-bottom: 20px;
}

.search-bar {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 20px;
  gap: 10px;
}

.search-bar select {
  padding: 10px;
  border-radius: 5px;
  border: none;
  font-size: 16px;
}

.character-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 20px;
}

.grid-item {
  width: 100%;
}

.character-list {
  margin-bottom: 30px;
  color: white;
}

.character-list h3 {
  text-align: center;
  margin-bottom: 10px;
}

.character-list ul {
  list-style: none;
  padding: 0;
  text-align: center;
}

.character-list li {
  padding: 5px 0;
  font-size: 16px;
}

@media (max-width: 900px) {
  .character-grid {
    grid-template-columns: 1fr;
  }

  .search-bar {
    flex-direction: column;
  }

  .character-list li {
    font-size: 14px;
  }
}
</style>