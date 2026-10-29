<template>
  <section class="comments">
    <h2 class="title">Заметки о питомце {{ petName }}</h2>

    <ul v-if="comments.length" class="comment-list">
      <li v-for="comment in comments" :key="comment.id" class="comment">
        <p class="comment-author">{{ comment.author }}</p>
        <p class="comment-text">{{ comment.text }}</p>
      </li>
    </ul>
    <p v-else class="empty">Пока нет заметок. Добавьте первую после смены.</p>

    <form class="form" @submit.prevent="submit">
      <label class="field">
        <span class="label">Ваше имя</span>
        <input v-model.trim="author" type="text" class="input" placeholder="Например, Аня" />
      </label>
      <label class="field">
        <span class="label">Заметка</span>
        <textarea
          v-model.trim="text"
          class="input textarea"
          rows="3"
          placeholder="Как прошла смена, поведение, аппетит…"
        ></textarea>
      </label>
      <p v-if="showError" class="error">Заполните имя и текст заметки</p>
      <button type="submit" class="submit">Добавить заметку</button>
    </form>
  </section>
</template>

<script>
export default {
  name: 'CommentSection',
  props: {
    petName: {
      type: String,
      required: true,
    },
    comments: {
      type: Array,
      required: true,
    },
  },
  emits: ['add-comment'],
  data() {
    return {
      author: '',
      text: '',
      showError: false,
    }
  },
  methods: {
    submit() {
      if (!this.author || !this.text) {
        this.showError = true
        return
      }
      this.$emit('add-comment', { author: this.author, text: this.text })
      this.text = ''
      this.showError = false
    },
  },
}
</script>

<style scoped>
.comments {
  display: flex;
  flex-direction: column;
  gap: var(--space-4);
  padding: var(--space-5);
  border-radius: var(--radius-xl);
  background: var(--color-paper-raised);
  box-shadow: 0 2px 10px rgba(20, 21, 26, 0.08);
}

.title {
  margin: 0;
  font-size: 20px;
  font-weight: 700;
}

.comment-list {
  display: flex;
  flex-direction: column;
  gap: var(--space-3);
  margin: 0;
  padding: 0;
  list-style: none;
}

.comment {
  padding: var(--space-3) var(--space-4);
  border-radius: var(--radius-l);
  background: var(--color-paper);
}

.comment-author {
  margin: 0 0 var(--space-1);
  font-size: 14px;
  font-weight: 600;
}

.comment-text {
  margin: 0;
  font-size: 15px;
  line-height: 1.4;
  color: var(--color-ink-soft);
}

.empty {
  margin: 0;
  color: var(--color-ink-faint);
}

.form {
  display: flex;
  flex-direction: column;
  gap: var(--space-3);
}

.field {
  display: flex;
  flex-direction: column;
  gap: var(--space-1);
}

.label {
  font-size: 14px;
  font-weight: 500;
}

.input {
  padding: var(--space-3) var(--space-4);
  border: 1.5px solid var(--color-line);
  border-radius: var(--radius-m);
  background: var(--color-paper-raised);
  font-size: 15px;
  color: var(--color-ink);
}

.input:focus {
  outline: none;
  border-color: var(--color-primary);
}

.textarea {
  resize: vertical;
}

.error {
  margin: 0;
  padding: var(--space-2) var(--space-3);
  border-radius: var(--radius-s);
  background: var(--color-error-bg);
  font-size: 14px;
  color: var(--color-ink);
}

.submit {
  height: 44px;
  border: none;
  border-radius: var(--radius-m);
  background: var(--color-primary);
  font-size: 15px;
  font-weight: 600;
  color: var(--color-ink);
  cursor: pointer;
}

.submit:hover {
  background: var(--color-primary-hover);
}

.submit:active {
  background: var(--color-primary-press);
}
</style>
