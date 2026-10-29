<template>
  <article class="card" :class="{ selected }">
    <div class="photo">
      <img v-if="pet.imageUrl" :src="pet.imageUrl" :alt="pet.name" class="photo-img" />
      <img v-else :src="pawIcon" alt="" class="placeholder" />

      <span v-if="pet.status === 'urgent'" class="tag tag-urgent">срочно</span>
      <span v-else-if="pet.status === 'treatment'" class="tag tag-treatment">на лечении</span>
      <span v-else class="tag tag-ready">готов к пристройству</span>

      <button
        type="button"
        class="favorite"
        :aria-label="pet.isFavorite ? 'Убрать из избранного' : 'Добавить в избранное'"
        :aria-pressed="pet.isFavorite"
        @click="$emit('toggle-favorite', pet.id)"
      >
        <img :src="pet.isFavorite ? heartFilledIcon : heartIcon" alt="" class="favorite-icon" />
      </button>
    </div>

    <div class="body">
      <h3 class="name">{{ pet.name }}</h3>
      <p class="description">{{ pet.description }}</p>
      <button type="button" class="notes-button" @click="$emit('select', pet.id)">
        Заметки волонтёров ({{ pet.comments.length }})
      </button>
    </div>
  </article>
</template>

<script>
import heartIcon from '../assets/icons/heart.svg'
import heartFilledIcon from '../assets/icons/heart-filled.svg'
import pawIcon from '../assets/icons/paw.svg'

export default {
  name: 'PetCard',
  props: {
    pet: {
      type: Object,
      required: true,
    },
    selected: {
      type: Boolean,
      default: false,
    },
  },
  emits: ['toggle-favorite', 'select'],
  data() {
    return {
      heartIcon,
      heartFilledIcon,
      pawIcon,
    }
  },
}
</script>

<style scoped>
.card {
  overflow: hidden;
  border: 2px solid transparent;
  border-radius: var(--radius-xl);
  background: var(--color-paper-raised);
  box-shadow: 0 2px 10px rgba(20, 21, 26, 0.08);
  transition: border-color 0.15s;
}

.card.selected {
  border-color: var(--color-primary);
}

.photo {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  aspect-ratio: 16 / 9;
  background: var(--color-line);
}

.photo-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.placeholder {
  width: 56px;
  opacity: 0.35;
}

.tag {
  position: absolute;
  top: var(--space-3);
  left: var(--space-3);
  padding: 6px 14px;
  border-radius: 999px;
  font-family: var(--font-mono);
  font-size: 13px;
}

.tag-urgent {
  background: var(--color-urgent);
}

.tag-treatment {
  background: var(--color-ai);
}

.tag-ready {
  background: var(--color-primary);
}

.favorite {
  position: absolute;
  top: var(--space-3);
  right: var(--space-3);
  display: flex;
  align-items: center;
  justify-content: center;
  width: 40px;
  height: 40px;
  padding: 0;
  border: none;
  border-radius: 50%;
  background: var(--color-paper-raised);
  cursor: pointer;
}

.favorite-icon {
  width: 22px;
  height: 22px;
  transition: transform 0.15s;
}

.favorite:active .favorite-icon {
  transform: scale(0.85);
}

.body {
  display: flex;
  flex-direction: column;
  gap: var(--space-3);
  padding: var(--space-4) var(--space-5) var(--space-5);
}

.name {
  margin: 0;
  font-size: 22px;
  font-weight: 700;
}

.description {
  margin: 0;
  font-size: 16px;
  line-height: 1.4;
  color: var(--color-ink-soft);
}

.notes-button {
  height: 40px;
  border: 1.5px solid var(--color-line);
  border-radius: var(--radius-m);
  background: var(--color-paper-raised);
  font-size: 15px;
  font-weight: 600;
  color: var(--color-ink);
  cursor: pointer;
  transition: background-color 0.15s, border-color 0.15s;
}

.notes-button:hover {
  background: var(--color-line);
  border-color: var(--color-line-strong);
}
</style>
