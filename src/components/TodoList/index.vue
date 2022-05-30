<template>
  <ul class="todos">
    <li
      v-for="todo in filteredTodos"
      :key="todo.id"
      @dblclick="handleDblClickTodo(todo)"
      class="todo"
    >
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
        <input v-model="todo.title" @blur="doneEditTitle(todo)" class="title" />
        <input
          v-if="todo.comment !== ''"
          v-model="todo.comment"
          placeholder="Введите комментарий"
          class="comment"
          @blur="doneEditComment(todo)"
          :ref="'comment' + todo.id"
        />
      </div>
      <button @click="handleDeleteTodo(todo.id)" class="delete">Удалить</button>
    </li>
  </ul>
  <div v-if="todos.length > 0" class="sideMenu">
    <ul class="filters">
      <li
        v-for="li in list"
        :key="li.name"
        @click="handleChangeVisibility(li)"
        :class="{ active: visibility === li.value }"
      >
        {{ li.name }}
      </li>
    </ul>
    <button
      v-if="selectedUsers.length > 0"
      @click="handleDeleteTodos"
      class="delete"
    >
      Удалить выбранные
    </button>
  </div>
</template>

<script>
export default {
  name: 'TodoList',
  props: ['text'],

  data() {
    return {
      todos: [
        {
          id: 1,
          title: 'Something',
          comment: '',
        },
      ],
      selectedUsers: [],
      visibility: 'all',
      list: [
        { name: 'Все', value: 'all' },
        { name: 'Активные', value: 'active' },
        { name: 'Завершенные', value: 'completed' },
      ],
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
      this.todos.push({
        id: this.todos.length + 1,
        title: text.trim(),
        comment: '',
      });
    },

    doneEditTitle(todo) {
      todo.title = todo.title.trim();
      if (!todo.title) {
        this.handleDeleteTodo(todo.id);
      }
    },

    handleChangeVisibility(li) {
      this.visibility = li.value;
    },

    handleDblClickTodo(todo) {
      if (todo.comment === '') {
        todo.comment = ' ';
      }
      this.$nextTick(() => {
        this.$refs['comment' + todo.id][0].focus();
      });
    },

    doneEditComment(todo) {
      todo.comment = todo.comment.trim();
      if (todo.comment === ' ') {
        this.todo.comment = '';
      }
    },
  },

  computed: {
    filteredTodos() {
      switch (this.visibility) {
        case 'all':
          return this.todos;
        case 'active':
          return this.todos.filter(
            (todo) => !this.selectedUsers.includes(todo.id),
          );
        case 'completed':
          return this.todos.filter((todo) =>
            this.selectedUsers.includes(todo.id),
          );
      }
      return this.todos;
    },
  },
};
</script>

<style lang="scss" scoped src="./style/index.scss"></style>
