<template>
  <AppHeader :favorites-count="favoritesCount" />

  <main class="layout">
    <PetList
      :pets="pets"
      :selected-id="selectedId"
      @toggle-favorite="toggleFavorite"
      @select="selectedId = $event"
    />

    <aside class="side">
      <CommentSection
        v-if="selectedPet"
        :key="selectedPet.id"
        :pet-name="selectedPet.name"
        :comments="selectedPet.comments"
        @add-comment="addComment"
      />
      <p v-else class="hint">Нажмите «Заметки волонтёров» на карточке, чтобы открыть дневник питомца.</p>
    </aside>
  </main>
</template>

<script>
import AppHeader from './components/AppHeader.vue'
import PetList from './components/PetList.vue'
import CommentSection from './components/CommentSection.vue'
import barsikPhoto from './assets/pets/barsik.png'
import rexPhoto from './assets/pets/rex.jpg'

export default {
  name: 'App',
  components: {
    AppHeader,
    PetList,
    CommentSection,
  },
  data() {
    return {
      selectedId: 1,
      nextCommentId: 4,
      pets: [
        {
          id: 1,
          name: 'Барсик',
          description: 'Кот, 3 года. Ласковый, ладит с детьми, приучен к лотку.',
          imageUrl: barsikPhoto,
          status: 'urgent',
          isFavorite: true,
          comments: [
            { id: 1, author: 'Аня', text: 'Сегодня хорошо поел и сам подошёл погладиться' },
            { id: 2, author: 'Максим', text: 'Боится пылесоса' },
          ],
        },
        {
          id: 2,
          name: 'Ляля',
          description: 'Кошка, 1 год. Очень активная, ладит с детьми',
          imageUrl: '',
          status: 'treatment',
          isFavorite: false,
          comments: [{ id: 3, author: 'Оля', text: 'Принимает лекарства, швы заживают.' }],
        },
        {
          id: 3,
          name: 'Рекс',
          description: 'Пёс, 5 лет. Спокойный, знает команды, хорошо ходит на поводке.',
          imageUrl: rexPhoto,
          status: 'ready',
          isFavorite: false,
          comments: [],
        },
      ],
    }
  },
  computed: {
    selectedPet() {
      return this.pets.find((pet) => pet.id === this.selectedId) || null
    },
    favoritesCount() {
      return this.pets.filter((pet) => pet.isFavorite).length
    },
  },
  methods: {
    toggleFavorite(id) {
      const pet = this.pets.find((item) => item.id === id)
      pet.isFavorite = !pet.isFavorite
    },
    addComment({ author, text }) {
      this.selectedPet.comments.push({ id: this.nextCommentId, author, text })
      this.nextCommentId += 1
    },
  },
}
</script>

<style scoped>
.layout {
  display: grid;
  grid-template-columns: minmax(0, 420px) minmax(0, 1fr);
  align-items: start;
  gap: var(--space-6);
  max-width: 1040px;
  margin: 0 auto;
  padding: var(--space-6) var(--space-5);
}

.side {
  position: sticky;
  top: var(--space-5);
}

.hint {
  margin: 0;
  color: var(--color-ink-soft);
}

@media (max-width: 760px) {
  .layout {
    grid-template-columns: 1fr;
  }

  .side {
    position: static;
  }
}
</style>
