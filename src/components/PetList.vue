<template>
  <section class="list">
    <h2 class="title">Питомцы, которым нужен дом</h2>
    <PetCard
      v-for="pet in pets"
      :key="pet.id"
      :pet="pet"
      :selected="pet.id === selectedId"
      @toggle-favorite="$emit('toggle-favorite', $event)"
      @select="$emit('select', $event)"
    />
  </section>
</template>

<script>
import PetCard from './PetCard.vue'

export default {
  name: 'PetList',
  components: {
    PetCard,
  },
  props: {
    pets: {
      type: Array,
      required: true,
    },
    selectedId: {
      type: Number,
      default: null,
    },
  },
  emits: ['toggle-favorite', 'select'],
}
</script>

<style scoped>
.list {
  display: flex;
  flex-direction: column;
  gap: var(--space-4);
}

.title {
  margin: 0;
  font-size: 24px;
  font-weight: 700;
}
</style>
