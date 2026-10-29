<template>
  <header class="header">
    <img :src="logo" alt="Лапки" class="logo" />
    <p class="stats">
      <img :src="heartIcon" alt="" class="stats-icon" />
      В избранном: <strong>{{ favoritesCount }}</strong>
    </p>
  </header>
</template>

<script>
import logo from '../assets/icons/logo.svg'
import heartIcon from '../assets/icons/heart-filled.svg'

export default {
  name: 'AppHeader',
  props: {
    favoritesCount: {
      type: Number,
      required: true,
    },
  },
  data() {
    return {
      logo,
      heartIcon,
    }
  },
}
</script>

<style scoped>
.header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: var(--space-4);
  padding: var(--space-4) var(--space-5);
  background: var(--color-paper-raised);
  border-bottom: 1px solid var(--color-line);
}

.logo {
  height: 40px;
}

.stats {
  display: flex;
  align-items: center;
  gap: var(--space-2);
  margin: 0;
  font-size: 14px;
  color: var(--color-ink-soft);
}

.stats-icon {
  width: 20px;
  height: 20px;
}

.stats strong {
  color: var(--color-ink);
}
</style>
