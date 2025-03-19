<template>
  <input v-model="query" placeholder="Buscar" @input="$emit('search', query)" class="search-input" />
</template>

<script>
export default {
  data() {
    return {
      query: "",
    };
  },
};
</script>

<style scoped>
.search-input {
  padding: 10px;
  width: 80%;
  max-width: 400px;
  border-radius: 5px;
  border: none;
  font-size: 16px;
}
</style>
