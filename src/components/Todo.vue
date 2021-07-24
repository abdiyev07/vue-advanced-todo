<template>
  <div class="todo">
    <div class="todo__header">
      <span @click="open">Открыть</span>
    </div>
    <h3 class="todo__title">{{ todo.title }}</h3>
    <p class="todo__description">{{ todo.description }}</p>
    <p class="todo__deadline">
      Дата deadline'a: <span> {{ todo.deadline | formatDate }} </span>
    </p>
  </div>
</template>

<script>
export default {
  name: "Todo",
  props: {
    todo: {
      type: Object,
      required: true,
      default: () => ({}),
    },
  },

  methods: {
    open() {
      this.$router.push({
        name: "TodoDetailsPage",
        params: { id: this.todo.created_at },
      });
    },
  },

  filters: {
    formatDate(value) {
      return new Intl.DateTimeFormat("ru-RU", {
        year: "numeric",
        month: "numeric",
        day: "numeric",
      }).format(new Date(value));
    },
  },
};
</script>

<style lang="scss">
.todo {
  width: 400px;
  margin: 1rem auto;
  padding: 0.7rem;
  border: 1px solid black;
  border-radius: 8px;

  & h3,
  & p {
    margin: 0 0 0.5rem 0;
  }

  &__header {
    text-align: right;

    & span {
      font-style: italic;
      font-weight: 300;
      cursor: pointer;
    }
  }
}
</style>
