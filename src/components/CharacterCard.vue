<template>
  <div class="character-card">
    <div class="card-image">
      <img class="img-size" :src="character.image" :alt="`Imagem de ${character.name}`" />
    </div>
    <div class="card-info">
      <h3>{{ character.name }}</h3>
      <p>
        <strong>Status:</strong>
        <span class="status-indicator" :class="statusClass"></span>
        {{ character.status }}
      </p>
      <p><strong>Origem:</strong>
        <span class="margin-txt">{{ character.origin.name }}</span>
      </p>
      <p><strong>Espécie:</strong>
        <span class="margin-txt">{{ character.species }}</span>
      </p>
      <p><strong>Genero:</strong>
        <span class="margin-txt">{{ character.gender }}</span>
      </p>
      <div class="button-container">
        <button @click.stop="$emit('viewDetails', character)">Ver Detalhes</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['character'],
  computed: {
    statusClass() {
      switch (this.character.status.toLowerCase()) {
        case 'alive':
          return 'status-alive';
        case 'dead':
          return 'status-dead';
        default:
          return 'status-unknown';
      }
    }
  }
};
</script>

<style scoped>
.character-card {
  background: #222;
  padding: 15px;
  border-radius: 10px;
  color: white;
  transition: transform 0.3s ease-in-out, box-shadow 0.3s ease-in-out;
  cursor: pointer;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
  display: flex;
  flex-direction: row;
  align-items: center;
  margin-bottom: 20px;
  width: 100%;
  box-sizing: border-box;
}

.character-card:hover {
  transform: scale(1.02);
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.4);
}

.card-image {
  flex: 0 0 40%;
  margin-right: 15px;
}

.card-info {
  flex: 1;
  text-align: left;
  display: flex;
  flex-direction: column;
}
.margin-txt{
  margin-left: 10px;
}
.img-size {
  width: 100%;
  border-radius: 10px;
  object-fit: cover;
  aspect-ratio: 1/1;
}

h3 {
  margin-top: 0;
  margin-bottom: 10px;
  font-size: 1.2rem;
}

p {
  margin: 5px 0;
  font-size: 0.9rem;
  display: flex;
  align-items: center;
}

.status-indicator {
  display: inline-block;
  width: 10px;
  height: 10px;
  border-radius: 50%;
  margin-right: 8px;
  margin-left: 5px;
}

.status-alive {
  background-color: #55cc44;
  box-shadow: 0 0 5px #55cc44;
}

.status-dead {
  background-color: #d63d2e;
  box-shadow: 0 0 5px #d63d2e;
}

.status-unknown {
  background-color: #9e9e9e;
  box-shadow: 0 0 5px #9e9e9e;
}

.button-container {
  margin-top: 30px;
}

button {
  color: #00bcd4;
  background: none;
  border: 1px solid #00bcd4;
  padding: 8px 16px;
  border-radius: 5px;
  cursor: pointer;
  font-size: 14px;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #00bcd4;
  color: #222;
}

@media (max-width: 600px) {
  .character-card {
    flex-direction: column;
  }

  .card-image {
    flex: 0 0 auto;
    margin-right: 0;
    margin-bottom: 15px;
    width: 100%;
  }

  .card-info {
    text-align: center;
  }

  p {
    justify-content: center;
  }

  .button-container {
    display: flex;
    justify-content: center;
  }
}
</style>