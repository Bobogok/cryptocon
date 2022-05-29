<template>
  <ul class="todos">
    <li v-for="todo in todos" :key="todo.id" class="todo">
      <div class="checkbox">
        <input
          v-bind:value="todo.id"
          v-model="selectedUsers"
          type="checkbox"
          name="checkbox"
          :id="todo.id"
        />
      </div>
      <div class="content">
        <h2 class="title">{{ todo.title }}</h2>
        <p class="comment">{{ todo.comment }}</p>
      </div>
      <button @click="handleDeleteTodo(todo.id)" class="delete">Удалить</button>
    </li>
  </ul>
  <div v-if="selectedUsers.length > 0" class="sideMenu">
    <button @click="handleDeleteTodos" class="delete">Удалить выбранные</button>
  </div>
</template>

<script>
export default {
  name: 'TodoList',
  props: ['text'],

  data() {
    return {
      todos: [
        { id: 0, title: 'Title', comment: 'Comment' },
        { id: 1, title: 'Title', comment: 'Comment' },
        { id: 2, title: 'Title', comment: 'Comment' },
      ],
      selectedUsers: [],
      value: 0,
    };
  },

  methods: {
    handleDeleteTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
    },

    handleDeleteTodos() {
      this.todos = this.todos.filter(
        (todo) => !this.selectedUsers.includes(todo.id),
      );
      this.selectedUsers = [];
    },

    addTodo(text) {
      const lengthArr = this.todos.length;

      this.todos.push({
        id: lengthArr > 0 ? this.todos[lengthArr - 1] + 1 : 0,
        title: text,
        comment: '',
      });
    },
  },
};
</script>

<style lang="scss" scoped src="./style/index.scss"></style>
