<template>
  <MainLayout>
    <div class="form__group field">
      <input
        v-model="inputText"
        @keydown.enter="handleNewTodo"
        type="input"
        class="form__field"
        placeholder="Todo"
        name="Todo"
        id="name"
        required
      />
      <label for="name" class="form__label">Todo</label>
    </div>
    <TodosComponent ref="todos" :text="inputText" />
  </MainLayout>
</template>

<script>
import MainLayout from './layouts/MainLayout/index.vue';
import TodosComponent from './components/TodoList';

export default {
  name: 'App',
  data() {
    return {
      inputText: '',
    };
  },
  methods: {
    handleNewTodo() {
      this.$refs.todos.addTodo(this.inputText);
      this.inputText = '';
    },
  },

  components: { MainLayout, TodosComponent },
};
</script>

<style lang="scss" src="./assets/style/index.scss"></style>
